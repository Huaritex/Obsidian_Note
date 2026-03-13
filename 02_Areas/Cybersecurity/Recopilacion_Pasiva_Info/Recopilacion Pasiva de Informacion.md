
- Recoleccion de Informacion sobre un objetivo determinado sin que las actividades realizadas por el analista sean minimamente detectadas por dicho objetivo

- Dificil de realizar y a menudo proporiciona resultados poco concluyentes

- La manera habitual de recoleccion pasiva de informacion es mediante el acceso a la informacion almacenada en lugares publicos

- Raramente se utiliza de manera individual


# Hacking de Buscadores: Google Hacking

> Fuerza que todos los resultados pertencezcan a la url

```
site:page.com objetivo tipo_archivo
```

>Reduce el espacio de busqueda, el resultado sea un pdf 

```
site:page.com filetype:pdf
```

-> Operaciones Booleanas

```
"index of" / "chat/logs"
```

-> Informacion SQL

```
filetype:SQL "MySQL dump"
```

-> Que busque en el texto SQL

```
filetype:SQL "MySQL dump" (pass|password|passwd|pwd)
```

-> App Web con url especifica buscar una parte de la url

```
inurl:index.php?id=
```

-> Mas Sites

```
site:gov filetype:pdf allintitle:restricted
```

