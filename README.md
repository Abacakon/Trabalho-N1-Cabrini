# 🛡️ IDS com Árvores de Decisão em Python

Este projeto é um **sistema de detecção de intrusão (IDS)** desenvolvido em Python, que utiliza **árvores de decisão** para analisar pacotes de rede em tempo real e **bloquear automaticamente fontes suspeitas** com `iptables`.

---

## 🎯 Objetivo

O sistema monitora o tráfego UDP da rede e detecta padrões anômalos com base em:
- Tamanho do pacote
- Frequência de envio por IP
- Porta de destino

Quando detectado um comportamento suspeito, o IP de origem é **bloqueado temporariamente**.

---

## ✅ Conclusão

- Utiliza **Machine Learning** (árvore de decisão) para classificar tráfego.
- Opera em tempo real usando **Scapy**.
- Bloqueia IPs suspeitos via `iptables`.
- Gera e salva **logs detalhados** das detecções.

---

## ⚙️ Funcionamento

### 1. **Modelo de Machine Learning**
O classificador é treinado com:
```python
features = [[200, 10, 53], [1200, 300, 53], [180, 5, 123]]
labels = [0, 1, 0]  # 1 = suspeito
clf = tree.DecisionTreeClassifier()
clf.fit(features, labels)

**2. Análise em tempo real**
Pacotes UDP são capturados com Scapy.

Cada pacote é analisado: tamanho, frequência, porta.

O modelo decide se é suspeito.

**3. Bloqueio automático**
Se suspeito, o IP é bloqueado com:

bash
Copiar
Editar
iptables -A INPUT -s <IP> -p udp -j DROP
O bloqueio dura 15 segundos.

**4. Logs**
Toda ação é registrada com timestamp.

Logs são salvos em ids_log.txt ao encerrar o script.

🚀 Como usar
Instale as dependências:

bash
Copiar
Editar
pip install scapy numpy scikit-learn
Execute o IDS (como root):

bash
Copiar
Editar
sudo python3 ids(n° da versão).py
Use Ctrl+C para parar e salvar o log.

📁 Saída
Arquivo de log: ids_log.txt
