# cheatsheet-jq

## options

| Option               | Description                |
| ------               | -----------                |
| -c, --compact-output | output is on a single line |
| -r, --raw-output     | output is not quoted       |

## filters

```
echo '{"a":1,"b":2}' | jq '.a' # 1
echo '[1,2,3]' | jq '.[1]' # 2
echo '{"a": [1,2,3]}' | jq '.a[]' # 1\n2\n3
echo '{"a":1,"b":2, "c":3}' | jq '.a, .b' # 1\n2
echo '[{"a":1},{"a":2}]' | jq '.[] | .a' # 1\n2
seq 2 | jq '(.+1)*2' # 4\n6
echo '{"a":1,"b":2}' | jq -c '[.a, .b]' # [1,2]
echo '[1,2,3]' | jq -c '{ "a": .[0], "b": [.[]] }' # {"a":1,"b":[1,2,3]}
echo '[1,2]' | jq -c '{ "a": .[], "b": .[] }' # {"a":1,"b":1}\n{"a":1,"b":2}\n{"a":2,"b":1}\n{"a":2,"b":2}
echo '{"a":1,"b":2, "c":3}' | jq '{a}' # {"a":1}
echo '{"a":"1","b":2, "c":3}' | jq '{(.a): .b}' # {"1":2}
```
