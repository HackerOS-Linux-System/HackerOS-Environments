# HackerOS-Environments

Srodowiska graficzne (powloki / DE) dla HackerOS.

## Struktura

| Katalog        | Czym jest                                                                  | Zarzadzane przez            |
|----------------|------------------------------------------------------------------------------|------------------------------|
| `shells/slint` | Pasek/powloka napisana w HackerScript (`.hcs`), UI w Slint. Domyslny kompozytor docelowy: **labwc**. | `virus` (patrz root `Virus.hk`) |
| `cli`          | Narzedzie CLI tego repo.                                                      | `bytes` (patrz `cli/Bytes.hk`) |

Dwa rozne narzedzia budowania (`virus` i `bytes`) wspolzyja w jednym
repo celowo - `build.hl` woła oba po kolei.

## Budowanie

```
bytes build --release          # cli/ i pozostale czesci spod bytes
cd shells/slint && virus build --release
```

Wymagane w PATH: `cargo`, `rustc`, `virus` (patrz
[HackerScript](https://github.com/HackerOS-Linux-System/HackerScript)).

## Uruchamianie pod labwc

Zobacz `shells/slint/README.md` po wpis do autostartu labwc.
