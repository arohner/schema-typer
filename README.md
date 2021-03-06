schema-typer ![CircleCI Status][]
============

[CircleCI Status]: https://circleci.com/gh/circleci/schema-typer.png


Creates core.typed types from prismatic/schema definitions. Inspired by https://gist.github.com/c-spencer/6569571

```clojure
[arohner/schema-typer "0.2.10"]
```
Requires schema > 0.2.0


Motivation
==========
Q: Why the hell build this?

A: core.typed is good at compile-time validation. prismatic/schema is
good at run-time validation. schema-typer avoids duplication between your
core.type definition, and your schema definition. Having types for
schemas allows you to prove at compile-time that validation is
happening, at runtime.

Usage
=====
```clojure
(:require [schema.core :as s]
          [circle.schema-typer :refer (def-schema-alias def-validator)])

(def user-schema {:login String}) ;; define a normal prismatic schema

(def-schema-alias User user-schema)
;; defines (def-alias User (HMap :mandatory {:login String}))

(def-validator validate-user User user-schema)
;; defines
;; (t/ann validate-user [Any -> User])
;; (defn validate-user [x]
;;   (s/validate user-schema x))
```

Limitations
===========

The mapping from schema -> core.typed is incomplete, but it should be obvious how to extend. Patches welcome.

License
=======
EPL 1.0, the same as Clojure
