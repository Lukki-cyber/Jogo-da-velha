def criar_tabuleiro():
    return [[" " for _ in range(3)] for _ in range(3)]

def mostrar_tabuleiro(tabuleiro):
    print("\n  0   1   2")
    for i, linha in enumerate(tabuleiro):
        print(i, " | ".join(linha))
        if i < 2:
            print("  ---------")

def verificar_vitoria(tabuleiro, jogador):
    # Verifica linhas, colunas e diagonais
    for i in range(3):
        if all([tabuleiro[i][j] == jogador for j in range(3)]) or \
           all([tabuleiro[j][i] == jogador for j in range(3)]):
            return True
    if all([tabuleiro[i][i] == jogador for i in range(3)]) or \
       all([tabuleiro[i][2 - i] == jogador for i in range(3)]):
        return True
    return False

def verificar_empate(tabuleiro):
    return all([cell != " " for row in tabuleiro for cell in row])

def jogo_da_velha():
    tabuleiro = criar_tabuleiro()
    jogador_atual = "X"

    while True:
        mostrar_tabuleiro(tabuleiro)
        print(f"\nVez do jogador {jogador_atual}")
        try:
            linha = int(input("Escolha a linha (0, 1, 2): "))
            coluna = int(input("Escolha a coluna (0, 1, 2): "))
            if tabuleiro[linha][coluna] != " ":
                print("Posição ocupada! Tente novamente.")
                continue
        except (ValueError, IndexError):
            print("Entrada inválida! Tente novamente.")
            continue

        tabuleiro[linha][coluna] = jogador_atual

        if verificar_vitoria(tabuleiro, jogador_atual):
            mostrar_tabuleiro(tabuleiro)
            print(f"\n🎉 Jogador {jogador_atual} venceu!")
            break
        if verificar_empate(tabuleiro):
            mostrar_tabuleiro(tabuleiro)
            print("\nEmpate!")
            break

        jogador_atual = "O" if jogador_atual == "X" else "X"

# Executar o jogo
jogo_da_velha()
