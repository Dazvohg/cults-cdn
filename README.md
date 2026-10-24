# cults-cdn

Repo público que funciona como **almacén temporal de archivos** para [`cults3d-agent`](https://github.com/Dazvohg/cults3d-agent), el agente que publica diseños 3D en Cults3D.

## Para qué existe

Cults3D no recibe archivos subidos: baja los STL, 3MF e imágenes desde una URL pública. Por eso, al publicar un diseño, el agente:

1. sube los archivos a `tmp/<producto>-<fecha>/` de este repo;
2. espera a que sean accesibles de forma anónima (también por jsDelivr);
3. le pide a Cults3D que cree el diseño con esas URLs;
4. cuando Cults3D terminó de bajarlos, **borra todo** (un commit `cleanup tmp/...` por archivo).

Por eso el historial son pares `tmp upload` / `cleanup`, y `tmp/` tiene que estar vacío casi siempre.

## Reglas

- **No guardes nada acá.** Todo lo que esté en `tmp/` se puede borrar.
- **Tiene que ser público**: si fuera privado, Cults3D no podría descargar los archivos.
- **No subas archivos pagos que quieras mantener privados**: durante unos minutos son accesibles para cualquiera con la URL.
- El token del agente (`CDN_TOKEN`) es de acceso fino: solo este repo, solo *Contents: read & write*. Renovarlo antes de que venza (1 año).

Los diseños y el código están en `cults3d-agent`.
