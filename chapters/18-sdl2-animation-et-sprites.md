# SDL2 - Animation, Sprites et Collisions

## 1. Déplacer un objet

```c
#include <SDL2/SDL.h>

int main(int argc, char *argv[]) {
    SDL_Init(SDL_INIT_VIDEO);
    SDL_Window   *fen = SDL_CreateWindow("Animation", SDL_WINDOWPOS_CENTERED, SDL_WINDOWPOS_CENTERED, 800, 600, 0);
    SDL_Renderer *r   = SDL_CreateRenderer(fen, -1, SDL_RENDERER_ACCELERATED);

    int x = 400, y = 300;
    int vitesse = 5;

    const Uint8 *touches = SDL_GetKeyboardState(NULL);
    int en_cours = 1;
    SDL_Event event;

    while (en_cours) {
        while (SDL_PollEvent(&event))
            if (event.type == SDL_QUIT) en_cours = 0;

        SDL_PumpEvents();  // Rafraîchit l'état du clavier

        // Déplacement avec les touches
        if (touches[SDL_SCANCODE_UP]    && y > 0)       y -= vitesse;
        if (touches[SDL_SCANCODE_DOWN]  && y < 560)     y += vitesse;
        if (touches[SDL_SCANCODE_LEFT]  && x > 0)       x -= vitesse;
        if (touches[SDL_SCANCODE_RIGHT] && x < 760)     x += vitesse;

        // Dessin
        SDL_SetRenderDrawColor(r, 20, 20, 30, 255);
        SDL_RenderClear(r);

        SDL_SetRenderDrawColor(r, 79, 142, 247, 255);
        SDL_Rect joueur = {x, y, 40, 40};
        SDL_RenderFillRect(r, &joueur);

        SDL_RenderPresent(r);
        SDL_Delay(16);  // ~60 FPS
    }

    SDL_DestroyRenderer(r);
    SDL_DestroyWindow(fen);
    SDL_Quit();
    return 0;
}
```

---

## 2. Animation avec rebonds (balle)

```c
float bx = 400, by = 300;
float vx = 3.5f, vy = 2.5f;
int   rayon = 20;

// Dans la boucle :
bx += vx;
by += vy;

// Rebonds sur les bords
if (bx - rayon < 0 || bx + rayon > 800) vx = -vx;
if (by - rayon < 0 || by + rayon > 600) vy = -vy;
```

---

## 3. Détection de collision (AABB)

La méthode **AABB** (Axis-Aligned Bounding Box) compare deux rectangles.

```c
int collision(SDL_Rect a, SDL_Rect b) {
    return (a.x < b.x + b.w &&
            a.x + a.w > b.x &&
            a.y < b.y + b.h &&
            a.y + a.h > b.y);
}

// Utilisation
SDL_Rect joueur  = {px, py, 40, 40};
SDL_Rect obstacle = {200, 150, 60, 60};

if (collision(joueur, obstacle)) {
    printf("Collision !\n");
}
```

---

## 4. Spritesheet - Animation par frames

Un **spritesheet** est une image contenant plusieurs frames d'animation côte à côte.

```c
#include <SDL2/SDL.h>
#include <SDL2/SDL_image.h>

int main(int argc, char *argv[]) {
    SDL_Init(SDL_INIT_VIDEO);
    IMG_Init(IMG_INIT_PNG);

    SDL_Window   *fen = SDL_CreateWindow("Sprite", SDL_WINDOWPOS_CENTERED, SDL_WINDOWPOS_CENTERED, 800, 600, 0);
    SDL_Renderer *r   = SDL_CreateRenderer(fen, -1, SDL_RENDERER_ACCELERATED);

    SDL_Surface *surf  = IMG_Load("assets/personnage.png");
    SDL_Texture *sprite = SDL_CreateTextureFromSurface(r, surf);
    SDL_FreeSurface(surf);

    int frame_w = 64, frame_h = 64;   // Taille d'une frame
    int frames  = 4;                   // Nombre de frames
    int frame_courant = 0;
    int compteur = 0;                  // Compteur de ticks

    SDL_Rect src  = {0, 0, frame_w, frame_h};  // Source (spritesheet)
    SDL_Rect dest = {100, 200, frame_w, frame_h};  // Destination (écran)

    int en_cours = 1;
    SDL_Event event;

    while (en_cours) {
        while (SDL_PollEvent(&event))
            if (event.type == SDL_QUIT) en_cours = 0;

        // Changer de frame toutes les 8 boucles (~7.5 FPS d'animation)
        compteur++;
        if (compteur >= 8) {
            frame_courant = (frame_courant + 1) % frames;
            src.x         = frame_courant * frame_w;
            compteur      = 0;
        }

        SDL_SetRenderDrawColor(r, 20, 20, 30, 255);
        SDL_RenderClear(r);
        SDL_RenderCopy(r, sprite, &src, &dest);
        SDL_RenderPresent(r);
        SDL_Delay(16);
    }

    SDL_DestroyTexture(sprite);
    SDL_DestroyRenderer(r);
    SDL_DestroyWindow(fen);
    IMG_Quit();
    SDL_Quit();
    return 0;
}
```

---

## 5. Chronomètre et delta time

Pour un mouvement fluide indépendant du FPS :

```c
Uint32 temps_precedent = SDL_GetTicks();

// Dans la boucle :
Uint32 temps_actuel = SDL_GetTicks();
float  delta        = (temps_actuel - temps_precedent) / 1000.0f;  // En secondes
temps_precedent     = temps_actuel;

// Mouvement à 200 pixels/seconde
x += vitesse * delta;
y += vy * delta;
```

---

## 6. Son avec SDL_mixer

```c
#include <SDL2/SDL_mixer.h>

Mix_Init(MIX_INIT_MP3 | MIX_INIT_OGG);
Mix_OpenAudio(44100, MIX_DEFAULT_FORMAT, 2, 2048);

// Charger un effet sonore
Mix_Chunk *son = Mix_LoadWAV("assets/bip.wav");
Mix_PlayChannel(-1, son, 0);  // Jouer une fois

// Charger et jouer une musique de fond
Mix_Music *musique = Mix_LoadMUS("assets/theme.mp3");
Mix_PlayMusic(musique, -1);   // -1 = boucle infinie

// Nettoyage
Mix_FreeChunk(son);
Mix_FreeMusic(musique);
Mix_CloseAudio();
Mix_Quit();
```
