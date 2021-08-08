# amqp-routing-match
![CI](https://github.com/artie-owlet/amqp-routing-match/actions/workflows/ci.yaml/badge.svg)
![Coverage](https://github.com/artie-owlet/amqp-routing-match/actions/workflows/coverage.yaml/badge.svg)
![Lint](https://github.com/artie-owlet/amqp-routing-match/actions/workflows/lint.yaml/badge.svg)

---

## Install

```bash
npm install @artie-owlet/amqp-routing-match
```

## Usage

### topic

```javascript
import { TopicPattern } from '@artie-owlet/amqp-routing-match';

const serviceV1 = new TopicPattern('service.v1.*');
if (serviceV1.match('service.v1.log')) {
    // do smth
}

const serviceAll = new TopicPattern('service.#');
if (serviceAll.match('service.v1.log')) {
    // do smth
}
```

### headers

```javascript
import { HeadersPattern } from '@artie-owlet/amqp-routing-match';

const test1 = new HeadersPattern({
    'x-match': 'all',
    app: 'test',
    version: 1,
});

if (test1.match({
    app: 'test',
    version: 1,
})) {
    // do smth
}

const errorOrBeta = new HeadersPattern({
    'x-match': 'any',
    log: 'error',
    scope: 'beta',
});

if (errorOrBeta.match({
    log: 'error',
    scope: 'release',
})) {
    // do smth
}

if (errorOrBeta.match({
    log: 'debug',
    scope: 'beta',
})) {
    // do smth
}
```
