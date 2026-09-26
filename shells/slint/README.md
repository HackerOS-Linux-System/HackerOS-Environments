# slint-shell

Pasek/powloka HackerOS. Logika (launcher, lista pulpitow, uruchamianie
procesow) jest napisana w HackerScript (`.hcs`); warstwa UI korzysta
z [Slint](https://slint.dev) przez blok `native {Rust}` (patrz
`cmd/ui.hcs` - to jedyne miejsce, ktore musi byc Rustem, bo makro
`slint::slint!{}` jest dostepne tylko w Ruscie).

## Budowanie

```
virus build --release
```

Binarka wynikowa laduje pod `cache/` wygenerowanego przez `virus`
projektu Cargo (patrz `docs/VIRUS.md` w repo HackerScript po
szczegoly, gdzie dokladnie).

## Uruchamianie pod labwc

To zwykle okno Wayland (backend `winit` w Slint) - dziala pod kazdym
kompozytorem wlroots, w tym `labwc`, bez dodatkowej konfiguracji.
Zeby odpalalo sie automatycznie razem z sesja, dopisz do
`~/.config/labwc/autostart`:

```sh
/sciezka/do/slint-shell &
```

### Znany limit: to NIE jest jeszcze pasek "zadokowany" (layer-shell)

Dzisiaj okno jest zwyklym oknem toplevel (choc `no-frame: true` +
`always-on-top: true` w `ui.hcs` upodabniaja je do paska), a nie
prawdziwym paskiem `wlr-layer-shell` zarezerwowanym na krawedzi
ekranu. Docelowo wymaga to wpiecia protokolu `wlr-layer-shell` po
stronie Rusta (np. crate `layer-shell` / recznej integracji z
`winit`+`smithay-client-toolkit`) - poza zakresem tej rundy, patrz
TODO w `cmd/launcher.hcs`/`cmd/workspaces.hcs` po analogiczne, uczciwie
opisane ograniczenia (przelaczanie pulpitow pod `labwc` tez nie jest
dzis realnie podpiete, tylko logowane).

## Wymagania systemowe (runtime)

Slint (backend `winit`, domyslny) potrzebuje zwyklych bibliotek
klienta Wayland: `libwayland-client`, `libxkbcommon` (+ ich
odpowiedniki `-dev`/`-devel` na etapie kompilacji). `foot`, `firefox`,
`pcmanfm`, `swaylock` w domyslnej liscie launchera (`launcher.hcs`) to
tylko przyklady - podmien na to, co faktycznie masz zainstalowane.
