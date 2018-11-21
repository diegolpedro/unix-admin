## Configurar locales (configuraciones regionales) necesarios
<p>
Si nos encontramos con problemas de configuracion regional faltantes, podemos realizar lo siguiente.  

(tanto con sudo como con root) 
<p>

```
sudo vim /etc/locale.gen
sudo grep -v "^#" /etc/locale.gen 
sudo locale-gen
```

- Con la primer linea entraremos a la configuracion regional para descomentar las lineas necesarias.  
Ej: es_AR.UTF-8 UTF-8  
  
- Con la segunda confirmamos lo hecho en el primer paso. 

- Y con la tercera generamos archivo de localizaciones con los parametros descomentados en el paso 1.

Con ```locale -a``` vemos en cualquier momento que configuraciones regionales estan seteadas en el sistema.  
De haber hecho correctamente el procedimiento anterior, apareceran las configuraciones reginales adicionadas.
