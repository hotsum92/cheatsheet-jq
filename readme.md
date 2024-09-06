# cheatsheet-jq

## options

| Option               | Description                |
| -------------------- | -------------------------- |
| -c, --compact-output | output is on a single line |
| -r, --raw-output     | output is not quoted       |


```
echo '{"a":1,"b":2}' | jq -c                       # compact print
echo '["a","b"]' | jq -r '.[]'                     # not quoted
```

## basic

```
echo '{"a":1,"b":2}' | jq                          # pretty print
echo '{"a":1,"b":2}' | jq '.a'                     # specific key
echo '{"a":1,"b":2}' | jq '.["a"]'                 # specific key
echo '[1,2,3]' | jq '.[1]'                         # index
echo '[1,2,3]' | jq '.[-1]'                        # index
echo '[1,2,3]' | jq '.[1:3]'                       # index
echo '[1,2,3]' | jq '.[:2]'                        # index
echo '[1,2,3]' | jq '.[-2:]'                       # index
echo '{"a": [1,2,3]}' | jq '.a[]'                  # array
echo '{"a":1,"b":2}' | jq -c '[.a, .b]'            # array
echo '{"a":1,"b":2, "c":3}' | jq '.a, .b'          # listing
echo '[{"a":1},{"a":2}]' | jq '.[] | .a'           # listing
seq 2 | jq '(.+1)*2'                               # calculate
echo '[1,2,3]' | jq -c '{ "a": .[0], "b": [.[]] }' # {"a":1,"b":[1,2,3]}
echo '[1,2]' | jq -c '{ "a": .[], "b": .[] }'      # {"a":1,"b":1}\n{"a":1,"b":2}\n{"a":2,"b":1}\n{"a":2,"b":2}
echo '{"a":1,"b":2, "c":3}' | jq '{a}'             # {"a":1}
echo '{"a":"1","b":2, "c":3}' | jq '{(.a): .b}'    # {"1":2}
echo '[{"name":"JSON", "good":true}, {"name":"XML", "good":false}]' | jq -r '.[] | .name' # pipe
```

## function

## +, -, *, /, %

```
echo '{"a": 1, "b": 2}' | jq '.a + .b'             # 3
echo '{"a": [1,2], "b": [2,3]}' | jq '.a + .b'     # [1,2,2,3]
echo '{"a": 1, "b": 2}' | jq '.a - .b'             # -1
echo '{"a": [1,2], "b": [2,3]}' | jq '.a - .b'     # [1]
echo '{"a": 1, "b": 2}' | jq '.a / 2 * .b'         # 1
```

## 

```
echo '[-10, -1.1, -1e-1]' | jq 'map(abs)'                            # [10,1.1,0.1]
echo '[[1,2], "string", {"a":2}, null, -5]' | jq 'map(type)'         # ["array","string","object","null","number"]
echo '[[1,2], "string", {"a":2}, null, -5, "あ"]' | jq 'map(length)' # [ 2, 6, 1, 0, 5, 1 ]
echo '{"a":"1","b":2, "c":3}' | jq 'keys'                            # ["a","b","c"]
echo '[42,3,35]' | jq 'keys'                                         # 3
```
