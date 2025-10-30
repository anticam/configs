# Miller

### List CSV content

[Miller verbs](https://miller.readthedocs.io/en/6.15.0/10min/)

```shell
mlr --csv cat sample.csv
```

```shell
mlr --icsv --opprint cat sample.csv
```

### Change column content to lowercase
```shell
mlr --csv put '$col1 = tolower($col1); $col2 = tolower($col2); $col3 = tolower($col3)' sample.csv
```

or use column names
```shell
mlr --csv put '$ID = tolower($ID); $reserveID = tolower($reserveID); $blockID = tolower($blockID)' sample.csv
```

change column content in the same file, make a backup:
```shell
mlr -I --csv put '$ID = tolower($ID); $reserveID = tolower($reserveID); $blockID = tolower($blockID)' sample.csv
```



