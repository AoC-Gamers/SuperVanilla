# SuperVanilla V1.1
[EN] [translation](https://translate.google.com/translate?sl=es&tl=en&u=https://github.com/AoC-Gamers/supervanilla)

SuperVanilla es una configuración competitiva para Left 4 Dead 2 que ajusta varios aspectos del juego para hacerlo más equilibrado y divertido.

## Características

### Diferencia con ZoneMod
- Tank y Witch están habilitados en 2v2, 3v3 y 4v4 según las reglas de aparición de cada mapa. Ambos están deshabilitados en 1v1.
- No se aplica reducción de daño a las armas 'cuerpo a cuerpo' usadas en chargers.
- Se permite aparición de armas T2 y T3 en el mapa.
- Se reemplaza el sistema de bonus de zonemod por el oficial.
- Se permiten wallkicks.
- Se elimina la limitación de infectados comúnes por superviviente vomitado.
- Se eliminan las restricciones de hordas de infectados comunes provocadas por eventos del mapa (mapinfo.txt).

### Comunes y megahordas

SuperVanilla parte de los valores de ZoneMod y aplica el mismo incremento
al límite general de comunes y al tamaño de la megahorda. Suma dos por plaza
de superviviente en 1v1 y 2v2, y uno por plaza en 3v3 y 4v4.

| Formato | Incremento | Límite general de comunes | Tamaño de la megahorda |
| --- | ---: | ---: | ---: |
| 1v1 | +2 | 5 + 2 = **7** | 12 + 2 = **14** |
| 2v2 | +4 | 10 + 4 = **14** | 25 + 4 = **29** |
| 3v3 | +3 | 18 + 3 = **21** | 32 + 3 = **35** |
| 4v4 | +4 | 30 + 4 = **34** | 50 + 4 = **54** |

En los formatos reducidos, los ajustes de `mapcvars.txt` pueden reemplazar
el límite general de comunes en mapas concretos.

Correcciones a la witch
```sh
* La *Witch* puede perseguir a las víctimas hasta zonas seguras.
* Se corrige su patrullaje cuando deambula por el mapa.
* Se evita que pierda su objetivo aleatoriamente.
```

### Límites de armas

Las cuotas se aplican por grupo y por equipo de supervivientes. Son de dos
armas en 4v4 y 3v3 y de una en 2v2. El perfil 1v1 carece de cuotas propias.

| Rifles de asalto | Escopetas automáticas | Rifles de precisión |
| --- | --- | --- |
| rifle | autoshotgun | hunting_rifle |
| rifle_desert | shotgun_spas | sniper_scout |
| rifle_ak47 |  | sniper_awp |
| rifle_sg552 |  | sniper_military |

### Daño de armas
- Se aplica una reducción del 20% de daño al Tank para las siguientes armas:
```sh
| hunting_rifle | autoshotgun | shotgun_spas | rifle | rifle_desert | rifle_ak47 | rifle_sg552 |
```

- Se aplica una reducción del 30% de daño al Tank para:
```sh
| sniper_military |
```

- Se aplica una amplificación del 10% de daño al Tank para:
```sh
| sniper_scout | sniper_awp |
```

- Se modifica las estadísticas base de la 'sniper_scout'.
```sh
* Daño base: 105 -> 125 dmg
* Duración de recarga: 2.9s -> 2.0s
* Capacidad del cargador: 15 -> 10 balas
```

- Se modifica las estadísticas base de la 'sniper_awp'.
```sh
* Daño Base: 115 -> 145 dmg
* Duración de recarga: 3.66s -> 2.5s
* Capacidad del cargador: 20 -> 10 balas
```

## Instalación
1. SuperVanilla requiere el proyecto base [L4D2-Competitive-Rework](https://github.com/SirPlease/L4D2-Competitive-Rework). Descárgalo e instálalo primero.
2. Con GNU Make y Python 3.10 o posterior, genera el ZIP local con `make deps-smx`, `make build-smx` y `make release`.
3. Copia las rutas `cfg/` y `addons/sourcemod/` declaradas dentro del ZIP a `left4dead2/` en el servidor.
4. Verifica los proveedores indicados en [NOTICES.md](NOTICES.md) y registra el modo como se muestra abajo.

## Configuración

### Agregar modo de juego
Para habilitar *SuperVanilla* en las votaciones del servidor, edita el archivo `addons/sourcemod/configs/matchmodes.txt` y agrega:

```plaintext
"MatchModes"
{
    "Super Vanilla Configs"
    {
        "svanilla"
        {
            "name" "Super Vanilla"
        }
        "sv3v3"
        {
            "name" "3v3 Super Vanilla"
        }
        "sv2v2"
        {
            "name" "2v2 Super Vanilla"
        }
        "sv1v1"
        {
            "name" "1v1 Super Vanilla"
        }
    }
}
```
Luego, reinicia el servidor para aplicar los cambios.

## Contribuciones
Gracias por tu interés en contribuir a *SuperVanilla*, Puedes reportar problemas o sugerir mejoras a través de la [página de issues](https://github.com/AoC-Gamers/supervanilla/issues) o enviando un *pull request* en el [repositorio de GitHub](https://github.com/AoC-Gamers/supervanilla/pulls).

## Licencias y autoría

Las configuraciones de Confogl declaran CC BY-SA 3.0. Consulta
[NOTICES.md](NOTICES.md) para la procedencia, licencias de los plugins
y componentes pendientes de confirmar.
