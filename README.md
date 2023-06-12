# Apprendre Angular: Développez facilement votre première application avec TypeScript !

cours de 9 heures sur angular 

Chapitre 2 : Les Composants
mock-pokemons.ts

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
45
46
47
48
49
50
51
52
53
54
55
56
57
58
59
60
61
62
63
64
65
66
67
68
69
70
71
72
73
74
75
76
77
78
79
80
81
82
83
84
85
86
87
88
89
90
91
92
93
94
95
96
97
98
99
100
101
102
103
104
105
106
107
108
109
110
111
112
import { Pokemon } from './pokemon';
  
export const POKEMONS: Pokemon[] = [
    {
        id: 1,
        name: "Bulbizarre",
        hp: 25,
        cp: 5,
        picture: "https://assets.pokemon.com/assets/cms2/img/pokedex/detail/001.png",
        types: ["Plante", "Poison"],
        created: new Date()
    },
    {
        id: 2,
        name: "Salamèche",
        hp: 28,
        cp: 6,
        picture: "https://assets.pokemon.com/assets/cms2/img/pokedex/detail/004.png",
        types: ["Feu"],
        created: new Date()
    },
    {
        id: 3,
        name: "Carapuce",
        hp: 21,
        cp: 4,
        picture: "https://assets.pokemon.com/assets/cms2/img/pokedex/detail/007.png",
        types: ["Eau"],
        created: new Date()
    },
    {
        id: 4,
        name: "Aspicot",
        hp: 16,
        cp: 2,
        picture: "https://assets.pokemon.com/assets/cms2/img/pokedex/detail/013.png",
        types: ["Insecte", "Poison"],
        created: new Date()
    },
    {
        id: 5,
        name: "Roucool",
        hp: 30,
        cp: 7,
        picture: "https://assets.pokemon.com/assets/cms2/img/pokedex/detail/016.png",
        types: ["Normal", "Vol"],
        created: new Date()
    },
    {
        id: 6,
        name: "Rattata",
        hp: 18,
        cp: 6,
        picture: "https://assets.pokemon.com/assets/cms2/img/pokedex/detail/019.png",
        types: ["Normal"],
        created: new Date()
    },
    {
        id: 7,
        name: "Piafabec",
        hp: 14,
        cp: 5,
        picture: "https://assets.pokemon.com/assets/cms2/img/pokedex/detail/021.png",
        types: ["Normal", "Vol"],
        created: new Date()
    },
    {
        id: 8,
        name: "Abo",
        hp: 16,
        cp: 4,
        picture: "https://assets.pokemon.com/assets/cms2/img/pokedex/detail/023.png",
        types: ["Poison"],
        created: new Date()
    },
    {
        id: 9,
        name: "Pikachu",
        hp: 21,
        cp: 7,
        picture: "https://assets.pokemon.com/assets/cms2/img/pokedex/detail/025.png",
        types: ["Electrik"],
        created: new Date()
    },
    {
        id: 10,
        name: "Sabelette",
        hp: 19,
        cp: 3,
        picture: "https://assets.pokemon.com/assets/cms2/img/pokedex/detail/027.png",
        types: ["Normal"],
        created: new Date()
    },
    {
        id: 11,
        name: "Mélofée",
        hp: 25,
        cp: 5,
        picture: "https://assets.pokemon.com/assets/cms2/img/pokedex/detail/035.png",
        types: ["Fée"],
        created: new Date()
    },
    {
        id: 12,
        name: "Groupix",
        hp: 17,
        cp: 8,
        picture: "https://assets.pokemon.com/assets/cms2/img/pokedex/detail/037.png",
        types: ["Feu"],
        created: new Date()
    }
];
pokemon.ts

1
2
3
4
5
6
7
8
9
export class Pokemon {
  id: number;
  hp: number;
  cp: number;
  name: string;
  picture: string;
  types: Array<string>;
  created: Date;
}
Chapitre 3 : Les Templates
app.component.html

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
<h1 class='center'>Pokémons</h1>
<div class='container'>
<div class="row">
<div *ngFor='let pokemon of pokemons' class="col s6 m4">
  <div class="card horizontal" (click)="selectPokemon(pokemon)">
    <div class="card-image">
      <img [src]="pokemon.picture">
    </div>
    <div class="card-stacked">
      <div class="card-content">
        <p>{{ pokemon.name }}</p>
        <p><small>{{ pokemon.created }}</small></p>
      </div>
    </div>
  </div>
</div>
</div>
</div>
Chapitre 4 : Les Directives
border-card.directive.ts

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
import { Directive, ElementRef } from '@angular/core';
  
@Directive({
  selector: '[pkmnBorderCard]'
})
export class BorderCardDirective {
    constructor(private el: ElementRef) {
        this.setBorder('#f5f5f5');
        this.setHeight(180);
    }
  
    private setBorder(color: string) {
        let border = 'solid 4px ' + color;
        this.el.nativeElement.style.border = border;
    }
  
    private setHeight(height: number) {
        this.el.nativeElement.style.height = height + 'px';
    }
}
Chapitre 5 : Les Pipes
pokemon-type-color.pipe.ts

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
45
46
47
48
49
50
51
52
53
54
55
56
57
import { Pipe, PipeTransform } from '@angular/core';
  
/*
 * Affiche la couleur correspondant au type du pokémon.
 * Prend en argument le type du pokémon.
 * Exemple d'utilisation:
 *   {{ pokemon.type | pokemonTypeColor }}
*/
@Pipe({name: 'pokemonTypeColor'})
export class PokemonTypeColorPipe implements PipeTransform {
  transform(type: string): string {
  
    let color: string;
  
    switch (type) {
      case 'Feu':
        color = 'red lighten-1';
        break;
      case 'Eau':
        color = 'blue lighten-1';
        break;
      case 'Plante':
        color = 'green lighten-1';
        break;
      case 'Insecte':
        color = 'brown lighten-1';
        break;
      case 'Normal':
        color = 'grey lighten-3';
        break;
      case 'Vol':
        color = 'blue lighten-3';
        break;
      case 'Poison':
        color = 'deep-purple accent-1';
        break;
      case 'Fée':
        color = 'pink lighten-4';
        break;
      case 'Psy':
        color = 'deep-purple darken-2';
        break;
      case 'Electrik':
        color = 'lime accent-1';
        break;
      case 'Combat':
        color = 'deep-orange';
        break;
      default:
        color = 'grey';
        break;
    }
  
    return 'chip ' + color;
  
  }
}
Chapitre 6 : Les Routes
detail-pokemon.component.html

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
<div *ngIf="pokemon" class="row">
<div class="col s12 m8 offset-m2">
<h2 class="header center">{{ pokemon.name }}</h2>
<div class="card horizontal hoverable">
  <div class="card-image">
    <img [src]="pokemon.picture">
  </div>
  <div class="card-stacked">
    <div class="card-content">
      <table class="bordered striped">
        <tbody>
          <tr>
            <td>Nom</td>
            <td><strong>{{ pokemon.name }}</strong></td>
          </tr>
          <tr>
            <td>Points de vie</td>
            <td><strong>{{ pokemon.hp }}</strong></td>
          </tr>
          <tr>
            <td>Dégâts</td>
            <td><strong>{{ pokemon.cp }}</strong></td>
          </tr>
          <tr>
            <td>Types</td>
            <td>
              <span *ngFor="let type of pokemon.types" class="{{ type | pokemonTypeColor }}">{{ type }}</span>
            </td>
          </tr>
          <tr>
            <td>Date de création</td>
            <td><em>{{ pokemon.created | date:"dd/MM/yyyy" }}</em></td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="card-action">
      <a (click)="goBack()">Retour</a>
    </div>
  </div>
</div>
</div>
</div>
<h4 *ngIf='!pokemon' class="center">Aucun pokémon à afficher !</h4>
list-pokemon.component.html

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
<h1 class='center'>Pokémons</h1>
  <div class='container'>
    <div class="row">
    <div *ngFor='let pokemon of pokemons' class="col s6 m4">
      <div class="card horizontal" (click)="selectPokemon(pokemon)" pkmn-border-card>
        <div class="card-image">
          <img [src]="pokemon.picture">
        </div>
        <div class="card-stacked">
          <div class="card-content">
            <p>{{ pokemon.name }}</p>
            <p><small>{{ pokemon.created | date:"dd/MM/yyyy" }}</small></p>
            <span *ngFor='let type of pokemon.types' class="{{ type | pokemonTypeColor }}">{{ type }}</span>
          </div>
        </div>
      </div>
    </div>
    </div>
  </div>
page-not-found.component.ts

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
import { Component } from '@angular/core';
  
@Component({
    selector: 'page-404',
    template: `
    <div class='center'>
      <img src="http://assets.pokemon.com/assets/cms2/img/pokedex/full/035.png"/>
      <h1>Hey, cette page n'existe pas !</h1>
      <a routerLink="/pokemons" class="waves-effect waves-teal btn-flat">
        Retourner à l' accueil
      </a>
    </div>
  `
})
export class PageNotFoundComponent { }
Chapitre 7 : Les Modules
pokemons-routing.module.ts

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
import { NgModule }             from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
  
import { ListPokemonComponent }    from './list-pokemon.component';
import { DetailPokemonComponent }  from './detail-pokemon.component';
  
// Les routes du module Pokémon
const pokemonsRoutes: Routes = [
    { path: 'pokemons', component: ListPokemonComponent },
    { path: 'pokemon/:id', component: DetailPokemonComponent }
];
  
@NgModule({
    imports: [
        RouterModule.forChild(pokemonsRoutes)
    ],
    exports: [
        RouterModule
    ]
})
export class PokemonRoutingModule { }
Chapitre 9 : Les Formulaires
pokemon-form.component.html

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
45
46
47
48
49
50
51
52
53
54
55
56
57
58
59
60
61
62
63
64
65
66
67
68
69
70
71
72
73
74
75
76
77
78
79
80
81
82
83
<form *ngIf="pokemon" (ngSubmit)="onSubmit()" #pokemonForm="ngForm">
  <div class="row">
    <div class="col s8 offset-s2">
      <div class="card-panel">
  
        <!-- Pokemon name -->
        <div class="form-group">
          <label for="name">Nom</label>
          <input type="text" class="form-control" id="name"
                  required
                  pattern="^[a-zA-Z0-9àéèç]{1,25}$"
                 [(ngModel)]="pokemon.name" name="name"
                 #name="ngModel">
  
          <div [hidden]="name.valid || name.pristine"
                class="card-panel red accent-1">
                Le nom du pokémon est requis (1-25).
          </div>
        </div>
  
        <!-- Pokemon hp -->
        <div class="form-group">
          <label for="hp">Point de vie</label>
          <input type="number" class="form-control" id="hp"
                  required
                  pattern="^[0-9]{1,3}$"
                 [(ngModel)]="pokemon.hp" name="hp"
                 #hp="ngModel">
           <div [hidden]="hp.valid || hp.pristine"
                 class="card-panel red accent-1">
                 Les points de vie du pokémon sont compris entre 0 et 999.
           </div>
        </div>
  
        <!-- Pokemon cp -->
        <div class="form-group">
          <label for="cp">Dégâts</label>
          <input type="number" class="form-control" id="cp"
                  required
                  pattern="^[0-9]{1,2}$"
                 [(ngModel)]="pokemon.cp" name="cp"
                 #cp="ngModel">
           <div [hidden]="cp.valid || cp.pristine"
                 class="card-panel red accent-1">
                 Les dégâts du pokémon sont compris entre 0 et 99.
           </div>
        </div>
  
        <!-- Pokemon types -->
        <form class="form-group">
          <label for="types">Types</label>
          <p *ngFor="let type of types">
            <label>
              <input type="checkbox"
                class="filled-in"
                id="{{ type }}"
                [value]="type"
                [checked]="hasType(type)"
                [disabled]="!isTypesValid(type)"
                (change)="selectType($event, type)"/>
              <span [attr.for]="type">
                <div class="{{ type | pokemonTypeColor }}">
                  {{ type }}
                </div>
              </span>
            </label>
          </p>
        </form>
  
        <!-- Submit button -->
        <div class="divider"></div>
        <div class="section center">
          <button type="submit"
            class="waves-effect waves-light btn"
            [disabled]="!pokemonForm.form.valid">
            Valider</button>
        </div>
  
      </div>
    </div>
  </div>
</form>
<h3 *ngIf="!pokemon" class="center">Aucun pokémon à éditer...</h3>
Chapitre 10 : Effectuer des requêtes HTTP standards

loader.component.ts

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
import { Component } from '@angular/core';
  
@Component({
  selector: 'pkmn-loader',
  template: `
    <div class="preloader-wrapper big active">
      <div class="spinner-layer spinner-blue">
        <div class="circle-clipper left">
          <div class="circle"></div>
        </div><div class="gap-patch">
          <div class="circle"></div>
        </div><div class="circle-clipper right">
          <div class="circle"></div>
        </div>
      </div>
    </div>
  `
})
export class LoaderComponent {}
search-pokemon.component.html

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
<div class="row">
  <div class="col s12 m6 offset-m3">
    <div class="card">
      <div class="card-content">
        <div class="input-field">
          <input #searchBox (keyup)="search(searchBox.value)"
            placeholder="Rechercher un pokémon"/>
        </div>
  
        <div class="collection">
          <a *ngFor="let pokemon of pokemons$ | async"
            (click)="gotoDetail(pokemon)" class="collection-item">
            {{ pokemon.name }}
          </a>
        </div>
      </div>
    </div>
  </div>
</div>
Chapitre 11 : Effectuer des traitements asynchrones avec RxJS

loader.component.ts

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
import { Component } from '@angular/core';
  
@Component({
  selector: 'pkmn-loader',
  template: `
    <div class="preloader-wrapper big active">
      <div class="spinner-layer spinner-blue">
        <div class="circle-clipper left">
          <div class="circle"></div>
        </div><div class="gap-patch">
          <div class="circle"></div>
        </div><div class="circle-clipper right">
          <div class="circle"></div>
        </div>
      </div>
    </div>
  `
})
export class LoaderComponent {}
Chapitre 12 : Authentification
auth-guard.service.ts

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
import { Injectable } from '@angular/core';
import { CanActivate, Router, ActivatedRouteSnapshot, RouterStateSnapshot }
    from '@angular/router';
import { AuthService } from './auth.service';
  
@Injectable()
export class AuthGuard implements CanActivate {
  
    constructor(private authService: AuthService, private router: Router) { }
  
    canActivate(route: ActivatedRouteSnapshot, state: RouterStateSnapshot): boolean {
        let url: string = state.url;
        return this.checkLogin(url);
    }
  
    checkLogin(url: string): boolean {
        if (this.authService.isLoggedIn) { return true; }
        this.authService.redirectUrl = url;
        this.router.navigate(['/login']);
  
        return false;
    }
}
auth.service.ts

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
import { Injectable } from '@angular/core';
// RxJS 6
import { Observable, of } from 'rxjs';
import { tap, delay } from 'rxjs/operators';
  
@Injectable()
export class AuthService {
    isLoggedIn: boolean = false; // L'utilisateur est-il connecté ?
    redirectUrl: string; // où rediriger l'utilisateur après l'authentification ?
    // Une méthode de connexion
    login(name: string, password: string): Observable<boolean> {
        // Faites votre appel à un service d'authentification...
        let isLoggedIn = (name === 'pikachu' && password === 'pikachu');
  
        return of(true).pipe(
            delay(1000),
            tap(val => this.isLoggedIn = isLoggedIn)
        );
    }
  
    // Une méthode de déconnexion
    logout(): void {
        this.isLoggedIn = false;
    }
}
login.component.ts

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
45
46
47
48
49
50
51
52
53
54
55
56
57
58
59
60
61
62
63
64
65
66
67
68
69
import { Component } from '@angular/core';
import { Router } from '@angular/router';
import { AuthService } from './auth.service';
  
@Component({
    selector: 'login',
    template: `
    <div class='row'>
    <div class="col s12 m4 offset-m4">
    <div class="card hoverable">
      <div class="card-content center">
        <span class="card-title">Page de connexion</span>
        <p><em>{{message}}</em></p>
      </div>
            <form #loginForm="ngForm">
          <div>
                    <label for="name">Name</label>
            <input type="text" id="name" [(ngModel)]="name" name="name" required>
          </div>
          <div>
            <label for="password">Password</label>
            <input type="password" id="password" [(ngModel)]="password" name="password" required>
          </div>
        </form>
      <div class="card-action center">
        <a (click)="login()" class="waves-effect waves-light btn"  *ngIf="!authService.isLoggedIn">Se connecter</a>
        <a (click)="logout()" *ngIf="authService.isLoggedIn">Se déconnecter</a>
      </div>
    </div>
    </div>
    </div>
  `
})
export class LoginComponent {
    message: string = 'Vous êtes déconnecté. (pikachu/pikachu)';
    private name: string;
    private password: string;
  
    constructor(private authService: AuthService, private router: Router) { }
  
    // Informe l'utilisateur sur son authentfication.
    setMessage() {
        this.message = this.authService.isLoggedIn ?
            'Vous êtes connecté.' : 'Identifiant ou mot de passe incorrect.';
    }
  
    // Connecte l'utilisateur auprès du Guard
    login() {
        this.message = 'Tentative de connexion en cours ...';
        this.authService.login(this.name, this.password).subscribe(() => {
            this.setMessage();
            if (this.authService.isLoggedIn) {
                // Récupère l'URL de redirection depuis le service d'authentification
                // Si aucune redirection n'a été définis, redirige l'utilisateur vers la liste des pokemons.
                let redirect = this.authService.redirectUrl ? this.authService.redirectUrl : '/pokemon/all';
                // Redirige l'utilisateur
                this.router.navigate([redirect]);
            } else {
                this.password = '';
            }
        });
    }
  
    // Déconnecte l'utilisateur
    logout() {
        this.authService.logout();
        this.setMessage();
    }
}
