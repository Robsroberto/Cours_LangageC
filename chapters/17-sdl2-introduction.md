# SDL2 - Introduction et Configuration

## 1. Qu'est-ce que SDL2 ?

**SDL2** (Simple DirectMedia Layer) est une bibliothèque C open-source permettant de créer des applications graphiques multiplateformes : jeux 2D, simulateurs, interfaces interactives.

Elle gère :
- Fenêtres et rendu graphique (SDL2 core)
- Images PNG/JPG (SDL2_image)
- Texte et polices (SDL2_ttf)
- Son et musique (SDL2_mixer)
- Entrées clavier, souris, manette

---

## 2. Installation

### Linux (Ubuntu/Debian)

```bash
sudo apt-get install libsdl2-dev libsdl2-image-dev libsdl2-ttf-dev libsdl2-mixer-dev
```

### Windows avec MinGW

1. Télécharger `SDL2-devel-x.x.x-mingw.tar.gz` sur [libsdl.org](https://libsdl.org)
2. Extraire dans `C:/SDL2/`
3. Dans CodeBlocks : Paramètres > Compilateur > Dossiers d'inclusion : `C:/SDL2/include/SDL2`
4. Linker : ajouter `-lSDL2main -lSDL2`

### Compilation en ligne de commande

```bash
gcc main.c -o monapp -lSDL2 -lSDL2_image -lSDL2_ttf -lSDL2_mixer
```

---

## 3. Structure de base d'un programme SDL2

```c
#include <SDL2/SDL.h>
#include <stdio.h>

int main(int argc, char *argv[]) {

    // 1. Initialisation SDL
    if (SDL_Init(SDL_INIT_VIDEO) != 0) {
        printf("Erreur init : %s\n", SDL_GetError());
        return 1;
    }

    // 2. Créer la fenêtre
    SDL_Window *fenetre = SDL_CreateWindow(
        "Ma première fenêtre SDL2",
        SDL_WINDOWPOS_CENTERED,
        SDL_WINDOWPOS_CENTERED,
        800, 600,
        0
    );
    if (!fenetre) {
        printf("Erreur fenêtre : %s\n", SDL_GetError());
        SDL_Quit();
        return 1;
    }

    // 3. Créer le renderer (moteur de dessin 2D)
    SDL_Renderer *renderer = SDL_CreateRenderer(fenetre, -1, SDL_RENDERER_ACCELERATED);

    // 4. Boucle principale
    int en_cours = 1;
    SDL_Event event;

    while (en_cours) {
        // Gestion des événements
        while (SDL_PollEvent(&event)) {
            if (event.type == SDL_QUIT) en_cours = 0;
            if (event.type == SDL_KEYDOWN &&
                event.key.keysym.sym == SDLK_ESCAPE) en_cours = 0;
        }

        // Fond noir
        SDL_SetRenderDrawColor(renderer, 0, 0, 0, 255);
        SDL_RenderClear(renderer);

        // --- Zone de dessin ---

        // Afficher le rendu
        SDL_RenderPresent(renderer);
    }

    // 5. Nettoyage
    SDL_DestroyRenderer(renderer);
    SDL_DestroyWindow(fenetre);
    SDL_Quit();

    return 0;
}
```

---

## 4. Dessiner des formes

```c
// Changer la couleur de dessin (R, G, B, Alpha 0-255)
SDL_SetRenderDrawColor(renderer, 255, 100, 0, 255);  // Orange

// Point
SDL_RenderDrawPoint(renderer, 400, 300);

// Ligne
SDL_RenderDrawLine(renderer, 0, 0, 800, 600);

// Rectangle vide
SDL_Rect rect = {100, 100, 200, 150};
SDL_RenderDrawRect(renderer, &rect);

// Rectangle plein
SDL_RenderFillRect(renderer, &rect);
```

---

## 5. Gestion des événements

```c
SDL_Event event;
while (SDL_PollEvent(&event)) {

    switch (event.type) {
        case SDL_QUIT:
            en_cours = 0;
            break;

        case SDL_KEYDOWN:
            switch (event.key.keysym.sym) {
                case SDLK_ESCAPE: en_cours = 0;       break;
                case SDLK_UP:     printf("Haut\n");   break;
                case SDLK_DOWN:   printf("Bas\n");    break;
                case SDLK_LEFT:   printf("Gauche\n"); break;
                case SDLK_RIGHT:  printf("Droite\n"); break;
                case SDLK_SPACE:  printf("Espace\n"); break;
            }
            break;

        case SDL_MOUSEBUTTONDOWN:
            printf("Clic (%d, %d)\n",
                event.button.x, event.button.y);
            break;

        case SDL_MOUSEMOTION:
            // event.motion.x, event.motion.y
            break;
    }
}
```

---

## 6. Contrôle des FPS

```c
Uint32 debut = SDL_GetTicks();

// ... logique du jeu et dessin ...

Uint32 elapsed = SDL_GetTicks() - debut;
if (elapsed < 16)
    SDL_Delay(16 - elapsed);  // Limiter à ~60 FPS
```

---

## 7. Charger une image

```c
#include <SDL2/SDL_image.h>

IMG_Init(IMG_INIT_PNG | IMG_INIT_JPG);

SDL_Surface *surf = IMG_Load("assets/joueur.png");
SDL_Texture *tex  = SDL_CreateTextureFromSurface(renderer, surf);
SDL_FreeSurface(surf);

SDL_Rect dest = {100, 100, 64, 64};
SDL_RenderCopy(renderer, tex, NULL, &dest);

SDL_DestroyTexture(tex);
IMG_Quit();
```

---

## 8. Afficher du texte

```c
#include <SDL2/SDL_ttf.h>

TTF_Init();
TTF_Font *police = TTF_OpenFont("assets/arial.ttf", 24);

SDL_Color blanc = {255, 255, 255, 255};
SDL_Surface *surf = TTF_RenderText_Blended(police, "Bonjour !", blanc);
SDL_Texture *tex  = SDL_CreateTextureFromSurface(renderer, surf);

int w, h;
SDL_QueryTexture(tex, NULL, NULL, &w, &h);
SDL_Rect pos = {50, 50, w, h};
SDL_RenderCopy(renderer, tex, NULL, &pos);

SDL_FreeSurface(surf);
SDL_DestroyTexture(tex);
TTF_CloseFont(police);
TTF_Quit();
```
