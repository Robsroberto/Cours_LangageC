# SDL2 - Atelier : Jeu de Pong Complet en C

## Objectif

Construire un **jeu de Pong complet** en C avec SDL2 :
- Balle animée avec rebonds et accélération progressive
- Raquette joueur (clavier W/S) + IA adversaire
- Affichage du score en temps réel (SDL_ttf)
- Effets visuels : ligne centrale, lueur sur la balle

---

## Structure du projet

```
pong/
├── main.c
├── Makefile
└── assets/
    └── arial.ttf
```

---

## Code source complet

```c
#include <SDL2/SDL.h>
#include <SDL2/SDL_ttf.h>
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define W  800
#define H  600
#define RW 15
#define RH 90
#define BS 14
#define VR 6

typedef struct { float x, y, vx, vy; } Balle;
typedef struct { float x, y; int score; } Raquette;

void dessiner_rect(SDL_Renderer *r, int x, int y, int w, int h) {
    SDL_Rect rect = {x, y, w, h};
    SDL_RenderFillRect(r, &rect);
}

void afficher_score(SDL_Renderer *r, TTF_Font *f, int s1, int s2) {
    SDL_Color blanc = {255, 255, 255, 255};
    char buf[16];
    int w, h;

    sprintf(buf, "%d", s1);
    SDL_Surface *sv = TTF_RenderText_Blended(f, buf, blanc);
    SDL_Texture *tv = SDL_CreateTextureFromSurface(r, sv);
    SDL_QueryTexture(tv, NULL, NULL, &w, &h);
    SDL_Rect r1 = {W/4 - w/2, 20, w, h};
    SDL_RenderCopy(r, tv, NULL, &r1);
    SDL_FreeSurface(sv); SDL_DestroyTexture(tv);

    sprintf(buf, "%d", s2);
    sv = TTF_RenderText_Blended(f, buf, blanc);
    tv = SDL_CreateTextureFromSurface(r, sv);
    SDL_QueryTexture(tv, NULL, NULL, &w, &h);
    SDL_Rect r2 = {3*W/4 - w/2, 20, w, h};
    SDL_RenderCopy(r, tv, NULL, &r2);
    SDL_FreeSurface(sv); SDL_DestroyTexture(tv);
}

void reset_balle(Balle *b, int vers_droite) {
    b->x  = W / 2.0f;
    b->y  = H / 2.0f;
    b->vx = vers_droite ? 4.0f : -4.0f;
    b->vy = (rand() % 5 - 2) * 1.5f;
    if (b->vy == 0) b->vy = 2.0f;
}

int main(int argc, char *argv[]) {
    srand((unsigned)time(NULL));

    SDL_Init(SDL_INIT_VIDEO);
    TTF_Init();

    SDL_Window   *fen = SDL_CreateWindow("Pong - Empire du Web",
        SDL_WINDOWPOS_CENTERED, SDL_WINDOWPOS_CENTERED, W, H, 0);
    SDL_Renderer *r   = SDL_CreateRenderer(fen, -1, SDL_RENDERER_ACCELERATED);
    TTF_Font *police  = TTF_OpenFont("assets/arial.ttf", 48);

    Raquette j1 = {20,      H/2.0f - RH/2.0f, 0};
    Raquette j2 = {W - 35,  H/2.0f - RH/2.0f, 0};
    Balle balle;
    reset_balle(&balle, 1);

    const Uint8 *touches = SDL_GetKeyboardState(NULL);
    int en_cours = 1;
    SDL_Event event;

    while (en_cours) {
        while (SDL_PollEvent(&event))
            if (event.type == SDL_QUIT) en_cours = 0;

        SDL_PumpEvents();

        // Joueur 1 : W / S
        if (touches[SDL_SCANCODE_W] && j1.y > 0)            j1.y -= VR;
        if (touches[SDL_SCANCODE_S] && j1.y + RH < H)       j1.y += VR;

        // IA joueur 2
        float centre2 = j2.y + RH / 2.0f;
        if (centre2 < balle.y - 5 && j2.y + RH < H) j2.y += 4;
        if (centre2 > balle.y + 5 && j2.y > 0)      j2.y -= 4;

        // Déplacer la balle
        balle.x += balle.vx;
        balle.y += balle.vy;

        // Rebonds haut/bas
        if (balle.y <= 0)         { balle.y = 0;        balle.vy = -balle.vy; }
        if (balle.y + BS >= H)    { balle.y = H - BS;   balle.vy = -balle.vy; }

        // Collision raquette j1
        if (balle.x <= j1.x + RW &&
            balle.y + BS >= j1.y &&
            balle.y <= j1.y + RH &&
            balle.vx < 0) {
            balle.vx = -balle.vx * 1.05f;  // Accélération
            float impact = (balle.y + BS/2 - (j1.y + RH/2)) / (RH/2.0f);
            balle.vy = impact * 5.0f;
        }

        // Collision raquette j2
        if (balle.x + BS >= j2.x &&
            balle.y + BS >= j2.y &&
            balle.y <= j2.y + RH &&
            balle.vx > 0) {
            balle.vx = -balle.vx * 1.05f;
            float impact = (balle.y + BS/2 - (j2.y + RH/2)) / (RH/2.0f);
            balle.vy = impact * 5.0f;
        }

        // Vitesse max
        if (balle.vx >  12) balle.vx =  12;
        if (balle.vx < -12) balle.vx = -12;

        // Points
        if (balle.x < 0)  { j2.score++; reset_balle(&balle, 1);  SDL_Delay(500); }
        if (balle.x > W)  { j1.score++; reset_balle(&balle, 0);  SDL_Delay(500); }

        // ---- Rendu ----
        SDL_SetRenderDrawColor(r, 15, 15, 25, 255);
        SDL_RenderClear(r);

        // Ligne centrale pointillée
        SDL_SetRenderDrawColor(r, 50, 50, 70, 255);
        for (int i = 0; i < H; i += 20)
            SDL_RenderDrawLine(r, W/2, i, W/2, i + 10);

        // Raquettes
        SDL_SetRenderDrawColor(r, 79, 142, 247, 255);
        dessiner_rect(r, (int)j1.x, (int)j1.y, RW, RH);
        SDL_SetRenderDrawColor(r, 247, 100, 79, 255);
        dessiner_rect(r, (int)j2.x, (int)j2.y, RW, RH);

        // Balle
        SDL_SetRenderDrawColor(r, 255, 255, 255, 255);
        dessiner_rect(r, (int)balle.x, (int)balle.y, BS, BS);

        // Score
        if (police) afficher_score(r, police, j1.score, j2.score);

        SDL_RenderPresent(r);
        SDL_Delay(16);
    }

    if (police) TTF_CloseFont(police);
    SDL_DestroyRenderer(r);
    SDL_DestroyWindow(fen);
    TTF_Quit();
    SDL_Quit();
    return 0;
}
```

---

## Makefile

```makefile
CC     = gcc
CFLAGS = -Wall -O2
LIBS   = -lSDL2 -lSDL2_ttf

pong: main.c
	$(CC) $(CFLAGS) main.c -o pong $(LIBS)

clean:
	rm -f pong
```

---

## Extensions possibles

- **Menu principal** : état `MENU` / `JEU` / `FIN` avec SDL_ttf
- **Effets sonores** : `bip.wav` à chaque rebond avec SDL_mixer
- **Mode 2 joueurs** : raquette droite avec touches flèches
- **IA difficile** : prédire la trajectoire de la balle
- **Particules** : petits éclats quand la balle touche une raquette

---

## Récapitulatif du cours Langage C

| Module | Contenu |
|--------|---------|
| Bases | Types, variables, opérateurs, E/S |
| Contrôle | if/else, switch, while, for |
| Tableaux | Statiques, dynamiques (malloc) |
| Chaînes | string.h, manipulation de texte |
| Fonctions | Prototypes, récursivité, modules |
| Structures | struct, typedef, imbrication |
| Pointeurs | Adresses, déréférencement, arithmétique |
| Fichiers | fopen, fread, fwrite, fseek |
| Listes | Simple, double, circulaire |
| Piles/Files | LIFO, FIFO, applications |
| Arbres | ABR, parcours, hauteur |
| SDL2 | Fenêtres, dessin, événements, jeux |

> Bravo, tu maîtrises maintenant le Langage C de A à Z !
