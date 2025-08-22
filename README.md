# Codigo-sobre-onibus-Sesi-Senai
# Alex José das Neves Junior e Hariel Ramadan Mohamed

[contador_passageiros.py](https://github.com/user-attachments/files/21927702/contador_passageiros.py)def processar_viagem(linha):
    dados = linha.strip().split(",")[1:]  
    passageiros_atual = 0
    total_entradas = 0

    for ponto in dados:
        if ":" in ponto:
            entradas, saidas = map(int, ponto.split(":"))
            passageiros_atual += entradas - saidas
            total_entradas += entradas
            if passageiros_atual < 0:
                passageiros_atual = 0

    return total_entradas, passageiros_atual


def main():
    with open('out.csv', 'r') as arquivo:
        linhas = arquivo.readlines()

    tamanho_bloco = 10  
    totais_por_bloco = {}

    linha_num = 1
    for inicio in range(0, len(linhas), tamanho_bloco):
        fim = min(inicio + tamanho_bloco, len(linhas))
        soma_bloco = 0

        for linha in linhas[inicio:fim]:
            total_entradas, _ = processar_viagem(linha)
            soma_bloco += total_entradas

        totais_por_bloco[f"Linha {linha_num}"] = soma_bloco
        linha_num += 1

  
    bloco_maior = max(totais_por_bloco, key=totais_por_bloco.get)
    bloco_menor = min(totais_por_bloco, key=totais_por_bloco.get)

    print(f"Maior movimento: {bloco_maior} -> {totais_por_bloco[bloco_maior]} passageiros")
    print(f"Menor movimento: {bloco_menor} -> {totais_por_bloco[bloco_menor]} passageiros")


if __name__ == "__main__":
    main()

SlIDES: 


