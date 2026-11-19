# Base de ZoneMod para SuperVanilla

| Referencia | Valor |
| --- | --- |
| Base | [SirPlease/L4D2-Competitive-Rework](https://github.com/SirPlease/L4D2-Competitive-Rework) |
| Versión comparada | ZoneMod **v2.9.2b** |
| Revisión comparada | [`0390482d48ee87ba16ecb39490dc6f235dbdc1e0`](https://github.com/SirPlease/L4D2-Competitive-Rework/tree/0390482d48ee87ba16ecb39490dc6f235dbdc1e0/cfg/cfgogl) |
| Modo de destino | SuperVanilla **v1.1**, sobre Versus |

Los perfiles reducidos heredan los CFG compartidos de su modo principal. Los límites generales se leen en `confogl.cfg`. Los ajustes de `mapcvars.txt` pueden reemplazar el límite de comunes en mapas concretos.

| Formato | SuperVanilla | ZoneMod | Comunes SV / ZM | Megahorda SV / ZM |
| --- | --- | --- | --- | --- |
| 4v4 | [`svanilla`](../../cfg/cfgogl/svanilla/confogl.cfg) | `zonemod` | 34 / 30 | 54 / 50 |
| 3v3 | [`sv3v3`](../../cfg/cfgogl/sv3v3/confogl.cfg) | `zm3v3` | 21 / 18 | 35 / 32 |
| 2v2 | [`sv2v2`](../../cfg/cfgogl/sv2v2/confogl.cfg) | `zm2v2` | 14 / 10 | 29 / 25 |
| 1v1 | [`sv1v1`](../../cfg/cfgogl/sv1v1/confogl.cfg) | `zm1v1` | 7 / 5 | 14 / 12 |

## Apagado sincronizado

Los cuatro perfiles pasan por el [CFG compartido de apagado](../../cfg/cfgogl/svanilla/confogl_off.cfg). Tras restablecer los ajustes de Confogl, el CFG ejecuta `pm_unload_plugins refresh`. Plugin Manager lo aporta la base. Se verificaron las cuatro cadenas de apagado en el ZIP local.

## Reglas propias de SuperVanilla

| Área | Comportamiento de SuperVanilla |
| --- | --- |
| Jefes | Habilita Witch y su indicador de porcentaje en 4v4, 3v3 y 2v2. En esos tamaños, Tank está habilitado en ambos modos. En 1v1, ambos modos desactivan los dos jefes. El [filtro global](../../cfg/stripper/supervanilla/global_filters.cfg) conserva apariciones de Witch por script que ZoneMod filtra. |
| Armas T2 y T3 | Omite las conversiones de ZoneMod a armas de menor nivel. Declara una cuota de dos por grupo de rifles, escopetas automáticas y rifles de precisión en 4v4 y 3v3, y de una en 2v2. El CFG de 1v1 carece de reglas propias de cuota. |
| Daño y recarga | Desactiva el ajuste específico de daño cuerpo a cuerpo contra Charger con `l4d2_melee_damage_charger -1`. El [CFG compartido](../../cfg/cfgogl/svanilla/shared_settings.cfg) aplica multiplicadores contra Tank de `0.8` a Hunting Rifle, Autoshotgun, SPAS y cuatro rifles de asalto, `0.7` a Military Sniper y `1.1` a Scout y AWP. Scout usa 125 de daño y 2 s de recarga. AWP usa 145 y 2.5 s. Ambos cargadores tienen 10 balas. |
| Puntuación y movimiento | Usa el bonus oficial y omite el plugin de puntuación híbrida. El [CFG de carga](../../cfg/cfgogl/svanilla/shared_plugins.cfg) omite `l4d2_nobackjumps`, en línea con los wallkicks documentados, y añade `l4d2_steady_boost` para infectados. |
| Comunes y Boomer | Aumenta los límites generales de comunes y megahordas según el formato. En 4v4 conserva el ecualizador de hordas de Boomer y omite los cuatro valores explícitos de `boomer_horde_amount` que declara ZoneMod. |

El [mapa de producto](../../scripts/package/package-map.json) incluye cuatro plugins. [`Witch_Double_Startle_Fix`](../../addons/sourcemod/scripting/Witch_Double_Startle_Fix.sp) corrige el sobresalto doble de la Witch errante. [`witch_allow_in_safezone`](../../addons/sourcemod/scripting/witch_allow_in_safezone.sp) permite la persecución hacia zonas seguras. [`witch_prevent_target_loss`](../../addons/sourcemod/scripting/witch_prevent_target_loss.sp) evita la pérdida aleatoria del objetivo. [`l4d_reload_fix`](../../addons/sourcemod/scripting/l4d_reload_fix.sp) corrige la animación de recarga al cambiar el tamaño del cargador.

## Diferencias pendientes de revisión

| Área | Configuración vigente y punto pendiente |
| --- | --- |
| Mapas | Los cuatro `mapinfo.txt` de SuperVanilla tienen 213 entradas. Les faltan cinco capítulos de Dead Center 2025 y, frente a ZoneMod 4v4, cuatro entradas de Snowtown. También cambian rangos de aparición de jefes. Hay una clave `max_distance 500` duplicada en `l4d2_fallindeath01` y 13 comandos `static_witch_map` repetidos en el CFG compartido. Los seis ajustes de `mapcvars.txt` coinciden por tamaño en 1v1, 2v2 y 3v3. |
| Stripper | El [árbol de SuperVanilla](../../cfg/stripper/supervanilla) contiene 157 filtros por mapa y ZoneMod tiene 175. En 93 archivos compartidos se detectaron diferencias en líneas activas. Queda por revisar qué cambios pueden incorporarse sin alterar los spawns de armas y jefes del modo. |
| Balance compartido | SuperVanilla usa `pill_passer` y omite los rangos de aparición de píldoras. Difieren atributos de SMG, escopetas y Magnum, godframes del Hunter, colisión del Smoker con comunes y daño de golpe y roca del Tank. |
| README y CFG | El README indica 7 para la megahorda de 1v1, cuyo CFG fija 14, y generaliza las cuotas de armas y la aparición de jefes. Los cuatro `mapinfo.txt` conservan 25 entradas `horde_limit` cada uno. Queda por confirmar el comportamiento en partida y ajustar la documentación. |

La aceptación en SRCDS queda pendiente. Debe cubrir la carga, la aparición de armas y jefes en mapas representativos y la descarga del modo. [Guía de compilación y distribución](../build/README.md).
