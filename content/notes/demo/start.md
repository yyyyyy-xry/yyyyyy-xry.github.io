---
title: demo note
weight: 20
menu:
  notes:
    name: Demo Note
    identifier: notes-demo-demo-note
    parent: demo
    weight: 20
---

<!-- Variable -->

{{< note title="Demo1" >}}

1234这是正文

{{< /note >}}

<!-- Condition -->

{{< note title="Demo2" >}}

```bash
if [[ -z "$string" ]]; then
  echo "String is empty"
elif [[ -n "$string" ]]; then
  echo "String is not empty"
fi
```

{{< /note >}}
