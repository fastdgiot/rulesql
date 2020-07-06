rulesql
=====

Sql parser for parsing SQL clauses of emqx rule engine.

This is a temporary libray which will be moved to emqx-rule-engine project after finished.

Build
-----

    $ rebar3 compile

Map/Reduce on Lists or Maps
---------------------------

```
############ The payload:
payload = {
  a: "b,c",
  b: [
    1,
    2,
    3
  ],
  c: [
    4,
    5
  ]
}

############ The SQL:

SELECT

  tokens(payload.a, ',') as tks,
  lreduce((tk, result) =>
          maps_get(tk, payload) as l,
          result ++ l
       [], tks) as v

FROM

  "t/#"


############ The Output

{
  tks: ["b", "c"],
  v: [1,2,3,4,5]
}

```
