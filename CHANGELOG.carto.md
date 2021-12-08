# CARTO Mapnik Changelog

## 3.0.15.17

**Release date**: 2019-07-09

Changes:
 - Improve precision when outputting variables into Postgis plugin SQL queries.

## 3.0.15.16

**Release date**: 2019-05-20

Changes:
 - Fix a bug that broke marker's cache (3.0.15.15).

## 3.0.15.15

**Release date**: 2019-05-15

Changes:
 - Avoid undefined behaviour in poly_subpixel_subscale.

## 3.0.15.14

**Release date**: 2019-05-14

Changes:
 - Marker cache improvements
    - Fix sample_idx calculation with negative values.
    - Use atomics to handle the cache (multithreading).
    - Remove const cast and use mutable members instead.

 - Fix a change in behaviour introduced in 3.0.15.12 where negative values left shifted changed value. As `<<` is undefined for negative ints, it was changed for an equivalent division but the `agg` library relied on a certain behaviour (e.g. `(-2 << 256) == -1`).

 - Postgis plugin connection manager: Thread safety and remove password from the id from upstream.

 - Update dependencies:
    - libpq to 10.7 (was 9.6.2)
    - jpeg_turbo to 1.5.2 (was 1.5.1)
    - libpng to 1.6.37 (was 1.6.28)
    - libtiff to 4.0.8 (was 4.0.7)
    - sqlite to 3.21.0 (was 3.17.0)
    - libgdal 2.4.1 (was 2.1.3)
    - cairo 1.14.12 (was 1.14.8)
    - zlib to 1.2.11 (was 1.2.8)
    - proj to 5.2.0 (was 4.9.3)

## 3.0.15.13

**Release date**: 2019-04-09

Changes:
 - Avoid heap-buffer-overflow in agg::rasterizer_cells_aa<Cell>::sort_cells.

## 3.0.15.12

**Release date**: 2019-04-08

Changes:
 - Addressed multiple bugs related to ubsan. Sent upstream. It includes changing the behaviour of the debug symbolizer when the box starts outside of the tile (x or y less than 0), as now it will be clipped by size_t::lowest() (0).
 - Some other compiler warnings addressed.

## 3.0.15.11

**Release date**: 2019-04-05

Changes:
 - Backport fixes related to UBSan from upstream/master (not in 3.0.x).
 - Address some compiler warnings.
 - Fix UB in deps/agg. Sent upstream.

## 3.0.15.10

**Release date**: 2019-03-29

Changes:
 - Improve clip calculation to avoid issues when using offset.
 - Update to match upstream 3.0.22 (our release still is 3.0.15).
 - Test and build using Xenial and clang 5.0.0 (which was already the default in mason)
 - Switch to harfbuzz 1.4.4-ft (reverts the change in 3.0.15.3)
 - Backport compatibility patches (ICU, clang, boost).


## 3.0.15.9

**Release date**: 2018-05-14

Changes:
 - Fix bug that failed to place lines in the MarkerSymbolizer if its length is 0. Sent upstream.

## 3.0.15.8

**Release date**: 2018-05-07

Changes:
 - Qualify ICU types explicitly (ICU 61 Compatibility). Sent upstream.
 - Move markers cache from a global scope to a per map scope. Multiple improvements to increase lookup speed and avoid the need for mutexes.
 - Apply overlap optimization to `load_map_string` too. Generalized it to be used also for points and text. Sent upstream.
 - Use pkg-config to find FreeType2 if available (Freetype 2.9.1+ compatibility). Sent upstream.

## 3.0.15.7

**Release date**: 2018-04-02

Changes:
 - Metrics: Add metrics in the grid renderer
 - Metrics: Compatibily fix for older compilers (80ecf2741 by @dprophet)
 - Fix build issue with MAPNIK_THREADSAFE disabled. Sent upstream.
 - Metrics: Internal rework (no mutex, no tree) to improve performance
 - Metrics: Add metrics for feature types
 - Metrics: Add metrics to the agg renderer
 - Metrics: Add metrics for cache misses
 - Markers Symbolizer Caches: Add a map extra parameter `markers_symbolizer_caches_disabled` that can be set to true to disable them.
 - Markers cache: Use pointer to cached attributes as part of the key. Also avoid a double free.

## 3.0.15.6

**Release date**: 2018-03-06

Changes:
 - Fixed some issues with memory management of cache and calculation of cache keys.
 - Increased cache sampling_rate to 8, which makes visual tests more robust.
 - Bring back osx visual tests checks

## 3.0.15.5

**Release date**: 2018-03-01

Changes:
 - Improve precision of the marker symbolizer cache.
 - Travis: Run visual test with overwrite and upload differences to transfer.sh

## 3.0.15.4

**Release date**: 2018-02-22

Changes:
 - Use metrics without guards
 - Add docs/metrics.md
 - PostGIS: Variables in postgis SQL queries must now additionally be wrapped in `!` (refs [#29](https://github.com/CartoDB/mapnik/issues/29), [mapnik/#3618](https://github.com/mapnik/mapnik/pull/3618)):
```sql
-- Before
SELECT ... WHERE trait = @variable

-- Now
SELECT ... WHERE trait = !@variable!
```
 - Add an internal cache to the marker symbolizer in the agg renderer.

## 3.0.15.3

**Release date**: 2018-01-19

Changes:
 - Switch back to harfbuzz 1.3.0

## 3.0.15.2

**Release date**: 2018-01-04

Changes:
 - Enable metrics by default [2036217](https://github.com/CartoDB/mapnik/commit/20362178de4aab1d758ea19137037fcbb470ef83).


## 3.0.15.1

**Release date**: 2018-01-03

Changes:
 - Add this very changelog
 - Add metrics support. See [#3767](https://github.com/mapnik/mapnik/pull/3767)
 - Add support for U_ICU_VERSION_MAJOR_NUM >= 59 [#3729](https://github.com/mapnik/mapnik/issues/3729)
 - Fix travis CI [#24](https://github.com/CartoDB/mapnik/pull/24)


## 3.0.15.0

**Release date**: 2017-12-22

Vanilla Mapnik 3.0.15 in which the rest of the code is based upon. See https://github.com/mapnik/mapnik/blob/v3.0.15/CHANGELOG.md
