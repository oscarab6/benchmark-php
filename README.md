# Microservicio PHP · Benchmark de algoritmos

Microservicio en PHP del **proyecto global** de Prácticas Continuas (Máster en Ingeniería del Software, Universidad de Murcia).

Recibe un algoritmo clásico y un tamaño de entrada, lo ejecuta 5 veces y devuelve la **mediana** del tiempo de ejecución en milisegundos. El frontend del proyecto consulta este servicio y los de los demás lenguajes para comparar su rendimiento.

> **Estado:** en construcción. De momento el repositorio solo tiene la configuración; la API y el primer algoritmo (MergeSort) llegan en los siguientes PR.

## Contrato de la API

> Provisional: se debe consensuar con el resto de grupos.

```http
POST /api/v1/benchmark
Content-Type: application/json

{ "algorithm": "mergesort", "size": 10000 }
```

```json
{
  "language": "php",
  "algorithm": "mergesort",
  "size": 10000,
  "timeMs": 12.34,
  "runs": 5
}
```

Algoritmos previstos: `mergesort`, `quicksort`, `insertionsort`, `selectionsort`, `fibonacci` y `matmul`.

## Requisitos

- Git
- PHP 8.3 o superior, con las extensiones `mbstring`, `openssl`, `curl`, `dom` y `xml`
- Composer 2

## Puesta en marcha

```bash
git clone https://github.com/oscarab6/benchmark-php.git
cd benchmark-php
composer install
git config core.hooksPath .githooks   # activa el hook de pre-commit (una vez por clon)
```

## Formato del código

El estilo se basa en PSR-12 y se aplica con PHP-CS-Fixer:

```bash
composer cs:check   # comprueba el formato (falla si algo no cumple)
composer cs:fix     # lo corrige
```

El hook de pre-commit ejecuta `cs:fix` automáticamente en cada commit.

## Cómo contribuir

Consulta [CONTRIBUTING.md](CONTRIBUTING.md).
