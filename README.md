# stpatack
# Ataque STP Claim Root Attack

## Descripción

Este laboratorio demuestra cómo un atacante puede manipular el protocolo **Spanning Tree Protocol (STP)** enviando BPDUs falsificadas para proclamarse como **Root Bridge** de la red.

Al convertirse en Root Bridge, el atacante puede alterar la topología de la red, redirigir tráfico y provocar interrupciones o degradación del servicio.

> ⚠️ Este proyecto ha sido desarrollado exclusivamente para fines educativos y pruebas autorizadas en entornos de laboratorio. :contentReference[oaicite:0]{index=0}

---

# Objetivo del Laboratorio

- Comprender el funcionamiento de STP.
- Analizar el proceso de elección del Root Bridge.
- Demostrar un ataque STP Claim Root.
- Observar los cambios en la topología de red.
- Implementar mecanismos de protección contra ataques STP.

---

# Topología de Red

<img width="425" height="360" alt="image" src="https://github.com/user-attachments/assets/5862bdf0-c55a-4bc0-ad47-dd1e13808fe4" />

# Requisitos

## Software

- Python 3.x
- Scapy
- Kali Linux o Parrot OS
- Wireshark
- GNS3 o PNETLab

## Instalación

```bash
pip install scapy
```

---

# Funcionamiento del Script

El script realiza las siguientes acciones:

1. Construye una BPDU (Bridge Protocol Data Unit) falsa.
2. Utiliza una prioridad STP extremadamente baja (0).
3. Utiliza una dirección MAC falsa de alta prioridad.
4. Se anuncia como Root Bridge legítimo.
5. Envía BPDUs continuamente cada 2 segundos.
6. Fuerza a los switches a recalcular la topología.

---

# Características

- Generación de BPDUs falsas.
- Simulación de Root Bridge con prioridad 0.
- Envío automático cada 2 segundos.
- Ataque de Capa 2.
- Compatible con redes Cisco y entornos de laboratorio.

---

# Ejecución

Ejecutar el script con privilegios de administrador:

```bash
sudo python3 stp_claim_root.py

# ¿Cómo funciona el ataque?

Spanning Tree Protocol selecciona automáticamente un Root Bridge utilizando:

1. Prioridad del switch.
2. Dirección MAC.

El atacante envía BPDUs indicando:

```text
Prioridad = 0
MAC = 00:00:00:00:00:01
```

Como STP siempre selecciona el valor más bajo, los switches pueden considerar al atacante como el nuevo Root Bridge.

#contrameidda

configure terminal
interface ethernet 0/0
no switchport port-security
shutdown
no shutdown
exit
clear mac address-table dynamic
show spanning-tree
