[__prod__]: #
[{]: <region> (header)

[}]: #
[{]: <region> (body)
# CSS, SASS and Bootstrap

In this chapter we will add Twitter's bootstrap to our project, and add some style and layout to the project.

# Adding and importing Bootstrap 4

First, we need to add Bootstrap 4 to our project - so let's do that.

Run the following command in your Terminal:

    $ meteor npm install --save bootstrap@4.0.0-alpha.3

 Import Bootstrap's styles into your project:

[{]: <helper> (diff_step 18.2)
#### Step 18.2: Import bootstrap style into the main style file

##### Changed client/main.scss
```diff
@@ -1,4 +1,6 @@
 ┊1┊1┊@import "{}/node_modules/angular2-meteor-accounts-ui/build/login-buttons.scss";
+┊ ┊2┊@import "{}/node_modules/bootstrap/scss/bootstrap.scss";
+┊ ┊3┊
 ┊2┊4┊
 ┊3┊5┊.sebm-google-map-container {
 ┊4┊6┊  width: 400px;
```
[}]: #

# First touch of style

Now let's add some style! we will add navigation bar in the top of the page.

We will also add a container with the `router-outlet` to keep that content of the page:

[{]: <helper> (diff_step 18.3)
#### Step 18.3: Add bootstrap navbar

##### Changed client/imports/app/app.component.html
```diff
@@ -1,3 +1,6 @@
-┊1┊ ┊<div>
+┊ ┊1┊<nav class="navbar navbar-light bg-faded">
+┊ ┊2┊  <a class="navbar-brand" href="#">Socially</a>
+┊ ┊3┊</nav>
+┊ ┊4┊<div class="container-fluid">
 ┊2┊5┊  <router-outlet></router-outlet>
 ┊3┊6┊</div>🚫↵
```
[}]: #

# Moving things around

So first thing we want to do now, is to move the login buttons to another place - let's say that we want it as a part of the navigation bar.

So first let's remove it from it's current place (parties list), first the view:

[{]: <helper> (diff_step 18.4)
#### Step 18.4: Remove LoginButtons from a template

##### Changed client/imports/app/parties/parties-list.component.html
```diff
@@ -2,8 +2,6 @@
 ┊2┊2┊  <parties-form [hidden]="!user" style="float: left"></parties-form>
 ┊3┊3┊  <input type="text" #searchtext placeholder="Search by Location">
 ┊4┊4┊  <button type="button" (click)="search(searchtext.value)">Search</button>
-┊5┊ ┊  
-┊6┊ ┊  <login-buttons></login-buttons>
 ┊7┊5┊
 ┊8┊6┊  <h1>Parties:</h1>
```
[}]: #

And add it to the main component, which is the component that responsible to the navigation bar, so the view first:

[{]: <helper> (diff_step 18.5)
#### Step 18.5: Add login buttons to the navigation bar

##### Changed client/imports/app/app.component.html
```diff
@@ -1,5 +1,6 @@
 ┊1┊1┊<nav class="navbar navbar-light bg-faded">
 ┊2┊2┊  <a class="navbar-brand" href="#">Socially</a>
+┊ ┊3┊  <login-buttons class="pull-right"></login-buttons>
 ┊3┊4┊</nav>
 ┊4┊5┊<div class="container-fluid">
 ┊5┊6┊  <router-outlet></router-outlet>
```
[}]: #

# Fonts and FontAwesome

Meteor gives you the control of your `head` tag, so you can import fonts and add your `meta` tags.

We will add a cool font and add [FontAwesome](https://fortawesome.github.io/Font-Awesome/) style file, which also contains it's font:

[{]: <helper> (diff_step 18.6)
#### Step 18.6: Add fonts and FontAwesome

##### Changed client/index.html
```diff
@@ -1,5 +1,8 @@
 ┊1┊1┊<head>
+┊ ┊2┊  <meta name="viewport" content="width=device-width, initial-scale=1">
 ┊2┊3┊  <base href="/">
+┊ ┊4┊  <link href='http://fonts.googleapis.com/css?family=Muli:400,300' rel='stylesheet' type='text/css'>
+┊ ┊5┊  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.4.0/css/font-awesome.min.css">
 ┊3┊6┊</head>
 ┊4┊7┊<body>
 ┊5┊8┊  <app>Loading...</app>
```
[}]: #

# Some more style

So now we will take advantage of all Bootstrap's features - first let's update the layout of the form:

[{]: <helper> (diff_step 18.7)
#### Step 18.7: Update the new party form

##### Changed client/imports/app/parties/parties-form.component.html
```diff
@@ -1,15 +1,21 @@
-┊ 1┊  ┊<form [formGroup]="addForm" (ngSubmit)="addParty()">
-┊ 2┊  ┊  <label>Name</label>
-┊ 3┊  ┊  <input type="text" formControlName="name">
+┊  ┊ 1┊<form [formGroup]="addForm" (ngSubmit)="addParty()" class="form-inline">
+┊  ┊ 2┊  <fieldset class="form-group">
+┊  ┊ 3┊    <label for="partyName">Party name</label>
+┊  ┊ 4┊    <input id="partyName" class="form-control" type="text" formControlName="name" placeholder="Party name" />
 ┊ 4┊ 5┊
-┊ 5┊  ┊  <label>Description</label>
-┊ 6┊  ┊  <input type="text" formControlName="description">
+┊  ┊ 6┊    <label for="description">Description</label>
+┊  ┊ 7┊    <input id="description" class="form-control" type="text" formControlName="description" placeholder="Description">
 ┊ 7┊ 8┊
-┊ 8┊  ┊  <label>Location</label>
-┊ 9┊  ┊  <input type="text" formControlName="location">
+┊  ┊ 9┊    <label for="location_name">Location</label>
+┊  ┊10┊    <input id="location_name" class="form-control" type="text" formControlName="location" placeholder="Location name">
 ┊10┊11┊
-┊11┊  ┊  <label>Public</label>
-┊12┊  ┊  <input type="checkbox" formControlName="public">
-┊13┊  ┊  
-┊14┊  ┊  <button type="submit">Add</button>
-┊15┊  ┊</form>🚫↵
+┊  ┊12┊    <div class="checkbox">
+┊  ┊13┊      <label>
+┊  ┊14┊        <input type="checkbox" formControlName="public">
+┊  ┊15┊        Public
+┊  ┊16┊      </label>
+┊  ┊17┊    </div>
+┊  ┊18┊
+┊  ┊19┊    <button type="submit" class="btn btn-primary">Add</button>
+┊  ┊20┊  </fieldset>
+┊  ┊21┊</form>
```
[}]: #

And now the parties list:

[{]: <helper> (diff_step 18.8)
#### Step 18.8: Update parties list layout

##### Changed client/imports/app/parties/parties-list.component.html
```diff
@@ -1,44 +1,100 @@
-┊  1┊   ┊<div>
-┊  2┊   ┊  <parties-form [hidden]="!user" style="float: left"></parties-form>
-┊  3┊   ┊  <input type="text" #searchtext placeholder="Search by Location">
-┊  4┊   ┊  <button type="button" (click)="search(searchtext.value)">Search</button>
-┊  5┊   ┊
-┊  6┊   ┊  <h1>Parties:</h1>
-┊  7┊   ┊
-┊  8┊   ┊  <div>
-┊  9┊   ┊    <select #sort (change)="changeSortOrder(sort.value)">
+┊   ┊  1┊<div class="row">
+┊   ┊  2┊  <div class="col-md-12">
+┊   ┊  3┊    <div class="jumbotron">
+┊   ┊  4┊      <h3>Create a new party!</h3>
+┊   ┊  5┊      <parties-form [hidden]="!user"></parties-form>
+┊   ┊  6┊      <div [hidden]="user">You need to login to create new parties!</div>
+┊   ┊  7┊    </div>
+┊   ┊  8┊  </div>
+┊   ┊  9┊</div>
+┊   ┊ 10┊<div class="row ma-filters">
+┊   ┊ 11┊  <div class="col-md-6">
+┊   ┊ 12┊    <h3>All Parties:</h3>
+┊   ┊ 13┊    <form class="form-inline">
+┊   ┊ 14┊      <input type="text" class="form-control" #searchtext placeholder="Search by Location">
+┊   ┊ 15┊      <button type="button" class="btn btn-primary" (click)="search(searchtext.value)">Search</button>
+┊   ┊ 16┊      Sort by name: <select class="form-control" #sort (change)="changeSortOrder(sort.value)">
 ┊ 10┊ 17┊      <option value="1" selected>Ascending</option>
 ┊ 11┊ 18┊      <option value="-1">Descending</option>
 ┊ 12┊ 19┊    </select>
+┊   ┊ 20┊    </form>
+┊   ┊ 21┊  </div>
+┊   ┊ 22┊</div>
+┊   ┊ 23┊<div class="row">
+┊   ┊ 24┊  <div class="col-md-6">
+┊   ┊ 25┊    <ul class="list-group">
+┊   ┊ 26┊      <li class="list-group-item">
+┊   ┊ 27┊        <pagination-controls (pageChange)="onPageChanged($event)"></pagination-controls>
+┊   ┊ 28┊      </li>
+┊   ┊ 29┊      <li *ngFor="let party of parties | async"
+┊   ┊ 30┊          class="list-group-item ma-party-item">
+┊   ┊ 31┊        <div class="row">
+┊   ┊ 32┊          <div class="col-sm-8">
+┊   ┊ 33┊            <h2 class="ma-party-name">
+┊   ┊ 34┊              <a [routerLink]="['/party', party._id]">undefined</a>
+┊   ┊ 35┊            </h2>
+┊   ┊ 36┊            @ undefined
+┊   ┊ 37┊            <p class="ma-party-description">
+┊   ┊ 38┊              undefined
+┊   ┊ 39┊            </p>
+┊   ┊ 40┊          </div>
+┊   ┊ 41┊          <div class="col-sm-4">
+┊   ┊ 42┊            <button class="btn btn-danger pull-right" [hidden]="!isOwner(party)" (click)="removeParty(party)"><i
+┊   ┊ 43┊              class="fa fa-times"></i></button>
+┊   ┊ 44┊          </div>
+┊   ┊ 45┊        </div>
+┊   ┊ 46┊        <div class="row ma-party-item-bottom">
+┊   ┊ 47┊          <div class="col-sm-4">
+┊   ┊ 48┊            <div class="ma-rsvp-sum">
+┊   ┊ 49┊              <div class="ma-rsvp-amount">
+┊   ┊ 50┊                <div class="ma-amount">
+┊   ┊ 51┊                  undefined
+┊   ┊ 52┊                </div>
+┊   ┊ 53┊                <div class="ma-rsvp-title">
+┊   ┊ 54┊                  YES
+┊   ┊ 55┊                </div>
+┊   ┊ 56┊              </div>
+┊   ┊ 57┊              <div class="ma-rsvp-amount">
+┊   ┊ 58┊                <div class="ma-amount">
+┊   ┊ 59┊                  undefined
+┊   ┊ 60┊                </div>
+┊   ┊ 61┊                <div class="ma-rsvp-title">
+┊   ┊ 62┊                  MAYBE
+┊   ┊ 63┊                </div>
+┊   ┊ 64┊              </div>
+┊   ┊ 65┊              <div class="ma-rsvp-amount">
+┊   ┊ 66┊                <div class="ma-amount">
+┊   ┊ 67┊                  undefined
+┊   ┊ 68┊                </div>
+┊   ┊ 69┊                <div class="ma-rsvp-title">
+┊   ┊ 70┊                  NO
+┊   ┊ 71┊                </div>
+┊   ┊ 72┊              </div>
+┊   ┊ 73┊            </div>
+┊   ┊ 74┊          </div>
+┊   ┊ 75┊        </div>
+┊   ┊ 76┊      </li>
+┊   ┊ 77┊      <li class="list-group-item">
+┊   ┊ 78┊        <pagination-controls (pageChange)="onPageChanged($event)"></pagination-controls>
+┊   ┊ 79┊      </li>
+┊   ┊ 80┊    </ul>
+┊   ┊ 81┊  </div>
+┊   ┊ 82┊  <div class="col-md-6">
+┊   ┊ 83┊    <ul class="list-group">
+┊   ┊ 84┊      <li class="list-group-item">
+┊   ┊ 85┊        <sebm-google-map
+┊   ┊ 86┊          [latitude]="0"
+┊   ┊ 87┊          [longitude]="0"
+┊   ┊ 88┊          [zoom]="1">
+┊   ┊ 89┊          <div *ngFor="let party of parties | async">
+┊   ┊ 90┊            <sebm-google-map-marker
+┊   ┊ 91┊              *ngIf="party.location.lat"
+┊   ┊ 92┊              [latitude]="party.location.lat"
+┊   ┊ 93┊              [longitude]="party.location.lng">
+┊   ┊ 94┊            </sebm-google-map-marker>
+┊   ┊ 95┊          </div>
+┊   ┊ 96┊        </sebm-google-map>
+┊   ┊ 97┊      </li>
+┊   ┊ 98┊    </ul>
 ┊ 13┊ 99┊  </div>
-┊ 14┊   ┊
-┊ 15┊   ┊  <ul>
-┊ 16┊   ┊    <li *ngFor="let party of parties | async">
-┊ 17┊   ┊      <a [routerLink]="['/party', party._id]">undefined</a>
-┊ 18┊   ┊      <p>undefined</p>
-┊ 19┊   ┊      <p>undefined</p>
-┊ 20┊   ┊      <button [hidden]="!isOwner(party)" (click)="removeParty(party)">X</button>
-┊ 21┊   ┊      <div>
-┊ 22┊   ┊        Who is coming:
-┊ 23┊   ┊        Yes - undefined
-┊ 24┊   ┊        Maybe - undefined
-┊ 25┊   ┊        No - undefined
-┊ 26┊   ┊      </div>
-┊ 27┊   ┊    </li>
-┊ 28┊   ┊  </ul>
-┊ 29┊   ┊
-┊ 30┊   ┊  <sebm-google-map
-┊ 31┊   ┊    [latitude]="0"
-┊ 32┊   ┊    [longitude]="0"
-┊ 33┊   ┊    [zoom]="1">
-┊ 34┊   ┊    <div *ngFor="let party of parties | async">
-┊ 35┊   ┊      <sebm-google-map-marker
-┊ 36┊   ┊        *ngIf="party.location.lat"
-┊ 37┊   ┊        [latitude]="party.location.lat"
-┊ 38┊   ┊        [longitude]="party.location.lng">
-┊ 39┊   ┊      </sebm-google-map-marker>
-┊ 40┊   ┊    </div>
-┊ 41┊   ┊  </sebm-google-map>
-┊ 42┊   ┊
-┊ 43┊   ┊  <pagination-controls (pageChange)="onPageChanged($event)"></pagination-controls>
 ┊ 44┊100┊</div>🚫↵
```
[}]: #

# Styling components

We will create style file for each component.

So let's start with the parties list, and add some style (it's not that critical at the moment what is the effect of those CSS rules)

[{]: <helper> (diff_step 18.9)
#### Step 18.9: Add styles for PartiesList

##### Added client/imports/app/parties/parties-list.component.scss
```diff
@@ -0,0 +1,125 @@
+┊   ┊  1┊.ma-add-button-container {
+┊   ┊  2┊  button.btn {
+┊   ┊  3┊    background: $color3;
+┊   ┊  4┊    float: right;
+┊   ┊  5┊    margin-right: 5px;
+┊   ┊  6┊    outline: none;
+┊   ┊  7┊    i {
+┊   ┊  8┊      color: $color5;
+┊   ┊  9┊    }
+┊   ┊ 10┊  }
+┊   ┊ 11┊}
+┊   ┊ 12┊
+┊   ┊ 13┊.ma-parties-col {
+┊   ┊ 14┊  padding-top: 20px;
+┊   ┊ 15┊}
+┊   ┊ 16┊
+┊   ┊ 17┊.ma-filters {
+┊   ┊ 18┊  margin-bottom: 10px;
+┊   ┊ 19┊}
+┊   ┊ 20┊
+┊   ┊ 21┊.ma-party-item {
+┊   ┊ 22┊  .ma-party-name {
+┊   ┊ 23┊    margin-bottom: 20px;
+┊   ┊ 24┊    a {
+┊   ┊ 25┊      color: $color6;
+┊   ┊ 26┊      text-decoration: none !important;
+┊   ┊ 27┊      font-weight: 400;
+┊   ┊ 28┊    }
+┊   ┊ 29┊  }
+┊   ┊ 30┊  .ma-party-description {
+┊   ┊ 31┊    color: $color6;
+┊   ┊ 32┊    font-weight: 300;
+┊   ┊ 33┊    padding-left: 18px;
+┊   ┊ 34┊    font-size: 14px;
+┊   ┊ 35┊  }
+┊   ┊ 36┊
+┊   ┊ 37┊  .ma-remove {
+┊   ┊ 38┊    color: lighten($color7, 20%);
+┊   ┊ 39┊    position: absolute;
+┊   ┊ 40┊    right: 20px;
+┊   ┊ 41┊    top: 20px;
+┊   ┊ 42┊    &:hover {
+┊   ┊ 43┊      color: $color7;
+┊   ┊ 44┊    }
+┊   ┊ 45┊  }
+┊   ┊ 46┊
+┊   ┊ 47┊  .ma-party-item-bottom {
+┊   ┊ 48┊    padding-top: 10px;
+┊   ┊ 49┊    .ma-posted-by-col {
+┊   ┊ 50┊      .ma-posted-by {
+┊   ┊ 51┊        color: darken($color4, 30%);
+┊   ┊ 52┊        font-size: 12px;
+┊   ┊ 53┊      }
+┊   ┊ 54┊      .ma-everyone-invited {
+┊   ┊ 55┊        @media (max-width: 400px) {
+┊   ┊ 56┊          display: block;
+┊   ┊ 57┊          i {
+┊   ┊ 58┊            margin-left: 0px !important;
+┊   ┊ 59┊          }
+┊   ┊ 60┊        }
+┊   ┊ 61┊        font-size: 12px;
+┊   ┊ 62┊        color: darken($color4, 10%);
+┊   ┊ 63┊        i {
+┊   ┊ 64┊          color: darken($color4, 10%);
+┊   ┊ 65┊          margin-left: 5px;
+┊   ┊ 66┊        }
+┊   ┊ 67┊      }
+┊   ┊ 68┊    }
+┊   ┊ 69┊
+┊   ┊ 70┊    .ma-rsvp-buttons {
+┊   ┊ 71┊      input.btn {
+┊   ┊ 72┊        color: darken($color3, 20%);
+┊   ┊ 73┊        background: transparent !important;
+┊   ┊ 74┊        outline: none;
+┊   ┊ 75┊        padding-left: 0;
+┊   ┊ 76┊        &:active {
+┊   ┊ 77┊          box-shadow: none;
+┊   ┊ 78┊        }
+┊   ┊ 79┊        &:hover {
+┊   ┊ 80┊          color: darken($color3, 30%);
+┊   ┊ 81┊        }
+┊   ┊ 82┊        &.btn-primary {
+┊   ┊ 83┊          color: lighten($color3, 10%);
+┊   ┊ 84┊          border: 0;
+┊   ┊ 85┊          background: transparent !important;
+┊   ┊ 86┊        }
+┊   ┊ 87┊      }
+┊   ┊ 88┊    }
+┊   ┊ 89┊
+┊   ┊ 90┊    .ma-rsvp-sum {
+┊   ┊ 91┊      width: 160px;
+┊   ┊ 92┊      @media (min-width: 400px) {
+┊   ┊ 93┊        float: right;
+┊   ┊ 94┊      }
+┊   ┊ 95┊      @media (max-width: 400px) {
+┊   ┊ 96┊        margin: 0 auto;
+┊   ┊ 97┊      }
+┊   ┊ 98┊    }
+┊   ┊ 99┊    .ma-rsvp-amount {
+┊   ┊100┊      display: inline-block;
+┊   ┊101┊      text-align: center;
+┊   ┊102┊      width: 50px;
+┊   ┊103┊      .ma-amount {
+┊   ┊104┊        font-weight: bold;
+┊   ┊105┊        font-size: 20px;
+┊   ┊106┊      }
+┊   ┊107┊      .ma-rsvp-title {
+┊   ┊108┊        font-size: 11px;
+┊   ┊109┊        color: #aaa;
+┊   ┊110┊        text-transform: uppercase;
+┊   ┊111┊      }
+┊   ┊112┊    }
+┊   ┊113┊  }
+┊   ┊114┊}
+┊   ┊115┊
+┊   ┊116┊.ma-angular-map-col {
+┊   ┊117┊  .angular-google-map-container, .angular-google-map {
+┊   ┊118┊    height: 100%;
+┊   ┊119┊    width: 100%;
+┊   ┊120┊  }
+┊   ┊121┊}
+┊   ┊122┊
+┊   ┊123┊.search-form {
+┊   ┊124┊  margin-bottom: 1em;
+┊   ┊125┊}🚫↵
```
[}]: #

And now let's add SASS file for the party details:

[{]: <helper> (diff_step 18.10)
#### Step 18.10: Add styles for the party details page

##### Added client/imports/app/parties/party-details.component.scss
```diff
@@ -0,0 +1,32 @@
+┊  ┊ 1┊.ma-party-details-container {
+┊  ┊ 2┊  padding: 20px;
+┊  ┊ 3┊
+┊  ┊ 4┊  .angular-google-map-container {
+┊  ┊ 5┊    width: 100%;
+┊  ┊ 6┊    height: 100%;
+┊  ┊ 7┊  }
+┊  ┊ 8┊
+┊  ┊ 9┊  .angular-google-map {
+┊  ┊10┊    width: 100%;
+┊  ┊11┊    height: 400px;
+┊  ┊12┊  }
+┊  ┊13┊
+┊  ┊14┊  .ma-map-title {
+┊  ┊15┊    font-size: 16px;
+┊  ┊16┊    font-weight: bolder;
+┊  ┊17┊  }
+┊  ┊18┊
+┊  ┊19┊  .ma-invite-list {
+┊  ┊20┊    margin-top: 20px;
+┊  ┊21┊    margin-bottom: 20px;
+┊  ┊22┊
+┊  ┊23┊    h3 {
+┊  ┊24┊      font-size: 16px;
+┊  ┊25┊      font-weight: bolder;
+┊  ┊26┊    }
+┊  ┊27┊
+┊  ┊28┊    ul {
+┊  ┊29┊      padding: 0;
+┊  ┊30┊    }
+┊  ┊31┊  }
+┊  ┊32┊}🚫↵
```
[}]: #

import it into the main SASS file:

[{]: <helper> (diff_step 18.11)
#### Step 18.11: Add components styles in main style entry point

##### Changed client/main.scss
```diff
@@ -1,8 +1,44 @@
 ┊ 1┊ 1┊@import "{}/node_modules/angular2-meteor-accounts-ui/build/login-buttons.scss";
 ┊ 2┊ 2┊@import "{}/node_modules/bootstrap/scss/bootstrap.scss";
 ┊ 3┊ 3┊
+┊  ┊ 4┊$color1 : #2F2933;
+┊  ┊ 5┊$color2 : #01A2A6;
+┊  ┊ 6┊$color3 : #29D9C2;
+┊  ┊ 7┊$color4 : #BDF271;
+┊  ┊ 8┊$color5 : #FFFFA6;
+┊  ┊ 9┊$color6 : #2F2933;
+┊  ┊10┊$color7 : #FF6F69;
+┊  ┊11┊
+┊  ┊12┊html, body {
+┊  ┊13┊  height: 100%;
+┊  ┊14┊}
+┊  ┊15┊
+┊  ┊16┊body {
+┊  ┊17┊  background-color: #f8f8f8;
+┊  ┊18┊  font-family: 'Muli', sans-serif;
+┊  ┊19┊}
 ┊ 4┊20┊
 ┊ 5┊21┊.sebm-google-map-container {
-┊ 6┊  ┊  width: 400px;
-┊ 7┊  ┊  height: 400px;
-┊ 8┊  ┊}🚫↵
+┊  ┊22┊  width: 450px;
+┊  ┊23┊  height: 450px;
+┊  ┊24┊}
+┊  ┊25┊
+┊  ┊26┊.navbar {
+┊  ┊27┊  background-color: #ffffff;
+┊  ┊28┊  border-bottom: #eee 1px solid;
+┊  ┊29┊  color: $color3;
+┊  ┊30┊  font-family: 'Muli', sans-serif;
+┊  ┊31┊  a {
+┊  ┊32┊    color: $color3;
+┊  ┊33┊    text-decoration: none !important;
+┊  ┊34┊  }
+┊  ┊35┊
+┊  ┊36┊  .navbar-right-container {
+┊  ┊37┊    position: absolute;
+┊  ┊38┊    top: 17px;
+┊  ┊39┊    right: 17px;
+┊  ┊40┊  }
+┊  ┊41┊}
+┊  ┊42┊
+┊  ┊43┊@import "./imports/app/parties/parties-list.component";
+┊  ┊44┊@import "./imports/app/parties/party-details.component";🚫↵
```
[}]: #

And use those new cool styles in the view of the party details:

[{]: <helper> (diff_step 18.12)
#### Step 18.12: Update the layout of the party details page

##### Changed client/imports/app/parties/party-details.component.html
```diff
@@ -1,42 +1,61 @@
-┊ 1┊  ┊<form *ngIf="party" (submit)="saveParty()">
-┊ 2┊  ┊  <label>Name</label>
-┊ 3┊  ┊  <input [disabled]="!isOwner" type="text" [(ngModel)]="party.name" name="name">
+┊  ┊ 1┊<div class="row ma-party-details-container">
+┊  ┊ 2┊  <div class="col-sm-6 col-sm-offset-3">
+┊  ┊ 3┊    <legend>View and Edit Your Party Details:</legend>
+┊  ┊ 4┊    <form class="form-horizontal" *ngIf="party" (submit)="saveParty()">
+┊  ┊ 5┊      <div class="form-group">
+┊  ┊ 6┊        <label>Party Name</label>
+┊  ┊ 7┊        <input [disabled]="!isOwner" type="text" [(ngModel)]="party.name" name="name" class="form-control">
+┊  ┊ 8┊      </div>
 ┊ 4┊ 9┊
-┊ 5┊  ┊  <label>Description</label>
-┊ 6┊  ┊  <input [disabled]="!isOwner" type="text" [(ngModel)]="party.description" name="description">
+┊  ┊10┊      <div class="form-group">
+┊  ┊11┊        <label>Description</label>
+┊  ┊12┊        <input [disabled]="!isOwner" type="text" [(ngModel)]="party.description" name="description" class="form-control">
+┊  ┊13┊      </div>
 ┊ 7┊14┊
-┊ 8┊  ┊  <label>Location</label>
-┊ 9┊  ┊  <input [disabled]="!isOwner" type="text" [(ngModel)]="party.location.name" name="location">
+┊  ┊15┊      <div class="form-group">
+┊  ┊16┊        <label>Location name</label>
+┊  ┊17┊        <input [disabled]="!isOwner" type="text" [(ngModel)]="party.location.name" name="location" class="form-control">
+┊  ┊18┊      </div>
 ┊10┊19┊
-┊11┊  ┊  <button [disabled]="!isOwner" type="submit">Save</button>
-┊12┊  ┊  <a [routerLink]="['/']">Cancel</a>
-┊13┊  ┊</form>
+┊  ┊20┊      <div class="form-group">
+┊  ┊21┊        <button [disabled]="!isOwner" type="submit" class="btn btn-primary">Save</button>
+┊  ┊22┊        <a [routerLink]="['/']" class="btn">Back</a>
+┊  ┊23┊      </div>
+┊  ┊24┊    </form>
 ┊14┊25┊
-┊15┊  ┊<div *ngIf="isOwner || isPublic">
-┊16┊  ┊  <p>Users to invite:</p>
-┊17┊  ┊  <ul>
-┊18┊  ┊    <li *ngFor="let user of users | async">
-┊19┊  ┊      <div>undefined</div>
-┊20┊  ┊      <button (click)="invite(user)">Invite</button>
-┊21┊  ┊    </li>
-┊22┊  ┊  </ul>
-┊23┊  ┊</div>
+┊  ┊26┊    <ul class="ma-invite-list" *ngIf="isOwner || isPublic">
+┊  ┊27┊      <h3>
+┊  ┊28┊        Users to invite:
+┊  ┊29┊      </h3>
+┊  ┊30┊      <li *ngFor="let user of users | async">
+┊  ┊31┊        <div>undefined</div>
+┊  ┊32┊        <button (click)="invite(user)" class="btn btn-primary btn-sm">Invite</button>
+┊  ┊33┊      </li>
+┊  ┊34┊    </ul>
 ┊24┊35┊
-┊25┊  ┊<div *ngIf="isInvited">
-┊26┊  ┊  <h2>Reply to the invitation</h2>
-┊27┊  ┊  <input type="button" value="I'm going!" (click)="reply('yes')">
-┊28┊  ┊  <input type="button" value="Maybe" (click)="reply('maybe')">
-┊29┊  ┊  <input type="button" value="No" (click)="reply('no')">
-┊30┊  ┊</div>
+┊  ┊36┊    <div *ngIf="isInvited">
+┊  ┊37┊      <h2>Reply to the invitation</h2>
+┊  ┊38┊      <input type="button" class="btn btn-primary" value="I'm going!" (click)="reply('yes')">
+┊  ┊39┊      <input type="button" class="btn btn-warning" value="Maybe" (click)="reply('maybe')">
+┊  ┊40┊      <input type="button" class="btn btn-danger" value="No" (click)="reply('no')">
+┊  ┊41┊    </div>
 ┊31┊42┊
-┊32┊  ┊<sebm-google-map
-┊33┊  ┊  [latitude]="lat || centerLat"
-┊34┊  ┊  [longitude]="lng || centerLng"
-┊35┊  ┊  [zoom]="8"
-┊36┊  ┊  (mapClick)="mapClicked($event)">
-┊37┊  ┊  <sebm-google-map-marker
-┊38┊  ┊    *ngIf="lat && lng"
-┊39┊  ┊    [latitude]="lat"
-┊40┊  ┊    [longitude]="lng">
-┊41┊  ┊  </sebm-google-map-marker>
-┊42┊  ┊</sebm-google-map>🚫↵
+┊  ┊43┊    <h3 class="ma-map-title">
+┊  ┊44┊      Click the map to set the party location
+┊  ┊45┊    </h3>
+┊  ┊46┊
+┊  ┊47┊    <div class="angular-google-map-container">
+┊  ┊48┊      <sebm-google-map
+┊  ┊49┊        [latitude]="lat || centerLat"
+┊  ┊50┊        [longitude]="lng || centerLng"
+┊  ┊51┊        [zoom]="8"
+┊  ┊52┊        (mapClick)="mapClicked($event)">
+┊  ┊53┊        <sebm-google-map-marker
+┊  ┊54┊          *ngIf="lat && lng"
+┊  ┊55┊          [latitude]="lat"
+┊  ┊56┊          [longitude]="lng">
+┊  ┊57┊        </sebm-google-map-marker>
+┊  ┊58┊      </sebm-google-map>
+┊  ┊59┊    </div>
+┊  ┊60┊  </div>
+┊  ┊61┊</div>🚫↵
```
[}]: #


# Summary

So in this chapter of the tutorial we added the Bootstrap library and used it's layout and CSS styles.

We also learned how to integrate SASS compiler with Meteor and how to create isolated SASS styles for each component.
[}]: #
[{]: <region> (footer)
[{]: <helper> (nav_step)
| [< Previous Step](step17.md) | [Next Step >](step19.md) |
|:--------------------------------|--------------------------------:|
[}]: #
[}]: #