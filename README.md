# smn-datos

Paquete de las **alertas meteorológicas oficiales del SMN** (Servicio Meteorológico Nacional, licencia CC BY 4.0) para Pronóstico Convertilo.

- `smn.json`: el feed del SMN y el XML de cada alerta, con la hora de armado (`generado`). Lo escribe `.github/workflows/actualizar.yml` en un solo commit (reemplaza el anterior).
- Quien lo lee: `lib/alertas.ts` de https://pronostico.convertilo.com.ar. **Lo usa solo si tiene menos de 3 horas**; el pedido directo al SMN no responde desde Cloudflare. Si está viejo, la página dice «no pudimos consultar» (nunca «sin alertas»).
- Cuándo se actualiza: el proceso está programado cada 15 minutos, pero GitHub lo corre cada ~4,7 h de mediana (hasta ~10 h). Por eso el Worker del panel Controlalo lo dispara a mano (`workflow_dispatch`) cada 30 minutos. Si algún día se cambia o se apaga eso, las alertas vuelven a estar disponibles solo ~6 de cada 10 horas.
- **No borrar este repo ni cambiarle el nombre del proceso (`actualizar.yml`) ni la rama `main`**: Pronóstico y el refresco automático dependen de ellos.
