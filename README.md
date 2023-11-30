import csv
import os

lista_usuarios = []

class Usuário:
    def __init__(self,nome_de_usuário,senha,tipo_assinatura,max_perfil):
        self.nome_de_usuário = nome_de_usuário
        self.senha = senha
        self.tipo_assinatura = tipo_assinatura
        self.max_perfil = max_perfil
        self.lista_perfis = []
        
    def addPerfil(self,perfil):
        self.lista_perfis.append(perfil)

    def RemoverPerfil(self,indice):
       for i in range(len(usuario.lista_perfis)):
                    if i == indice:
                        usuario.lista_perfis.pop(i)
                        print("Perfil excluído com sucesso!")
        
for i  in range(len(lista_usuarios) - 1):
    print(lista_usuarios[i].nome_de_usuário)

class Perfil:
    def __init__(self,nome,idade):
        self.nome = nome
        self.idade = idade
        self.lista_favoritos = []
        self.lista_ultimos_assistidos = []


    def AdicionarFavorito(self,Mídia):
        self.lista_favoritos.append(Mídia)
    
    def AdicionarUltimos(self,ultimo):
        self.lista_ultimos_assistidos.append(ultimo)


    def RemoverFavorito(self,Mídia):
        for Mídia in self.lista_favoritos:
            self.lista_favoritos.exclude(Mídia)
        
class Mídia:
    def __init__(self,id,tipo,titulo,gênero,ano_lançamento,classificação,):
        self.id = id
        self.tipo = tipo
        self.titulo = titulo
        self.gênero = gênero
        self.ano_lançamento = ano_lançamento
        self.classificação = classificação
        


    def ExibirInfo(self):
        print('[ID] - ',self.id,'\n[TIPO] - ',self.tipo,'\n[TÍTULO] - ',self.titulo,'\n[GÊNERO] - ',self.gênero,'\n[ANO DE LANÇAMENTO] - ',self.ano_lançamento,'\n[CLASSIFICAÇÃO] - ',self.classificação)

class Série(Mídia):
    def __init__(self,id,tipo, titulo ,gênero,ano_lançamento,classificação,temp):
        super().__init__(id,tipo, titulo,gênero,ano_lançamento,classificação)
        self.temp = temp
        self.episódios = []
        
    
    def ExibirInfo(self):
        super().ExibirInfo()
        print('[TEMPORADAS] - ',self.temp)
    
    def Listar_ep(self,ep):
        self.ep.append(ep)

class Filme(Mídia):
    def __init__(self, id, tipo, titulo, gênero, ano_lançamento, classificação,Diretor,Produtor):
        super().__init__(id, tipo, titulo, gênero, ano_lançamento, classificação)
        self.Diretor = Diretor
        self.Produtor = Produtor
    
    def ExibirInfo(self):
        super().ExibirInfo()
        print('[DIRETOR] - ',self.Diretor,'\n[PRODUTOR] - ',self.Produtor)

class Documentário(Mídia):
    def __init__(self, id, tipo, titulo, gênero, ano_lançamento, classificação,tema):
        super().__init__(id, tipo, titulo, gênero, ano_lançamento, classificação)
        self.tema = tema

    def ExibirInfo(self):
        super().ExibirInfo()
        print('[TEMA] - ',self.tema)

class Animação(Mídia):
    def __init__(self, id, tipo, titulo, gênero, ano_lançamento, classificação,estudio):
        super().__init__(id, tipo, titulo, gênero, ano_lançamento, classificação)
        self.estudio = estudio

    def ExibirInfo(self):
        super().ExibirInfo()
        print('[ESTÚDIO] - ',self.estudio)

class ProgramaTV(Mídia):
    def __init__(self, id, tipo, titulo, gênero, ano_lançamento, classificação):
        super().__init__(id, tipo, titulo, gênero, ano_lançamento, classificação)
        self.lista_eps = []
    
   

#PROGRAMA PRINCIPAL:
def menu_acesso():
    print('[1] - Acessar \n[2] - Criar Conta\n[3] - Sair')
    escolha = int(input('Digite a opção desejada: '))
    os.system('cls' if os.name == 'nt' else 'clear')
    return escolha

def menu_perfil():
    print('[1] - Alterar assinatura\n[2] - Acessar perfil\n[3] - Editar perfil\n[4] - Adicionar perfil\n[5] - Remover perfil\n[6] - Voltar ao menu anterior')
    escolha = int(input('Digite a opção desejada: '))
    os.system('cls' if os.name == 'nt' else 'clear')
    return escolha

def menu_Mídia():
    print('[1] - Buscar por nome\n[2] - Últimos assistidos\n[3] - Favoritos\n[4] - Filmes\n[5] - Séries\n[6] - Documentários\n[7] - Animações\n[8] - Programas de TV\n[9] - Voltar ao menu anterior')
    escolha = int(input('Digite a opção desejada: '))
    os.system('cls' if os.name == 'nt' else 'clear')
    return escolha

def verificarLogin(n_u,senha):
    U = open('usuariospoo2.csv')
    reader = csv.reader(U)
    data = list(reader)
    data.pop(0)
    U.close()
    for i in range(len(data)):
        if n_u in data[i] and senha in data[i]:
            return True
    else:
        return False
    
acessado = False
escolha = menu_acesso()

while escolha!=3:
    while acessado == False:
        if escolha == 1:
            n_u = input('Informe o nome do usuário: ')
            senha = input('Informe sua senha: ')
            verificar = verificarLogin(n_u,senha)
            if verificar == True:
                usuario = Usuário(n_u,senha,None,None) #Criação do objeto 
                U =open('usuariospoo2.csv')
                reader = csv.reader(U)
                for i in reader: #Instanciação do objeto
                    if n_u and senha in i:
                        usuario.nome_de_usuário = i[1]
                        usuario.senha = i[2]
                        usuario.tipo_assinatura = i[3]
                        if usuario.tipo_assinatura == 'Premium':
                            usuario.max_perfil = 5
                        else:
                            usuario.max_perfil = 3
                        lista_usuarios.append(usuario)
                        print('Acesso concluido')
                        print('Bem vinda',usuario.nome_de_usuário)
                        U.close()
                        acessado = True
                        break 
            else:
                print('nome ou senha errado')
        
        elif escolha == 2:

            nome_novaconta = input('Informe o nome de usuário da nova conta: ')
            senha_novaconta = input('Informe uma senha para sua nova conta: ')
            tipo_assinatura = input('[TIPOS DE ASSINATURA]\nSimples = RS:29,90\nPremium = RS:49,90\nInforme o tipo de assinatura desejada: ')
            max = 0
            if tipo_assinatura == 'Simples':
                max = 3
            else:
                max = 5
            usuario = Usuário(nome_novaconta,senha_novaconta,tipo_assinatura,max)
            U = open('usuariospoo2.csv','a')
            writer = csv.writer(U)
            writer.writerow([5,nome_novaconta,senha_novaconta,tipo_assinatura])
            U.close()
            escolha = menu_acesso()
        else:
            print('opção inválida, favor digitar outro número.')
            escolha = menu_acesso()
            break
    else:
        
        P = open('perfilpoo2.csv')
        reader = csv.reader(P)
        for i in reader:
            if usuario.nome_de_usuário in i:
                perfil = Perfil(None,None)
                perfil.nome = i[1]
                perfil.idade = i[2]
                for c in range(3,14):
                    perfil.AdicionarFavorito(i[c])
                for u in range(13,22):
                    perfil.AdicionarUltimos(i[u])
                usuario.lista_perfis.append(perfil)
                
        escolha_perfil = menu_perfil()
        while escolha_perfil != 6:
            if escolha_perfil == 1:
    
                if usuario.tipo_assinatura == 'Simples':
                    usuario.tipo_assinatura = 'Premium'
            
                    usuario.max_perfil = 5
                    
                    
                else:
                    usuario.tipo_assinatura = 'Simples'
                
                    usuario.max_perfil = 3
                    
                    
                print('Sua assinatura foi alterada com sucesso!')
                U = open('usuariospoo2.csv','r')
                reader = csv.reader(U)
                for i in reader:
                    if usuario.nome_de_usuário in i:
                        i[3] = usuario.tipo_assinatura
                        print(i)  #Atualiza o arq porém não aparece no arquivo em si
                U.close() 
                
                escolha_perfil = menu_perfil()

            elif escolha_perfil== 2:
                for i in range(len(usuario.lista_perfis)):
                    print(usuario.lista_perfis[i].nome)
                acessar_perfil = int(input('informe o índice do perfil a ser acessado: '))
                for i in range(len(usuario.lista_perfis)):
                    if acessar_perfil == i:
                        perfil = Perfil(usuario.lista_perfis[i].nome,usuario.lista_perfis[i].idade)
                        for c in range(len(usuario.lista_perfis[i].lista_favoritos)):
                            perfil.AdicionarFavorito(usuario.lista_perfis[i].lista_favoritos[c])
                        for l in range(len(usuario.lista_perfis[i].lista_ultimos_assistidos)):
                            perfil.AdicionarUltimos(usuario.lista_perfis[i].lista_ultimos_assistidos[l])
                        
                        print('perfil acessado')
                escolha_midia = menu_Mídia()
                while escolha_midia!= 9:
                    if escolha_midia == 1:
                        busca = input('Busca: ')
                        C = open('catalogo.csv')
                        reader = csv.reader(C)
                        midia = Mídia(None,None,None,None,None,None)
                        for i in reader:
                            if busca in i:
                                midia.id = i[0]
                                midia.tipo = i[1]
                                midia.titulo = i[2]
                                midia.gênero = i[3]
                                midia.ano_lançamento = i[4] 
                                midia.classificação = i[5]
                        C.close()
                        midia.ExibirInfo()
                        escolha_midia = menu_Mídia()
                    elif escolha_midia == 2:
                        C = open('catalogo.csv')
                        reader = csv.reader(C)
                        midia = Mídia(None,None,None,None,None,None)
                        for c in reader:
                            for i in range(len(perfil.lista_ultimos_assistidos)):
                                if perfil.lista_ultimos_assistidos[i] == c[0]:
                                    midia.id = c[0]
                                    midia.tipo = c[1]
                                    midia.titulo = c[2]
                                    midia.gênero = c[3]
                                    midia.ano_lançamento = c[4] 
                                    midia.classificação = c[5]
                                    midia.ExibirInfo()
                            
                        C.close
                        escolha_midia = menu_Mídia()
                        
                    elif escolha_midia == 3:
                         C = open('catalogo.csv')
                         reader = csv.reader(C)
                         midia = Mídia(None,None,None,None,None,None)
                         for c in reader:
                             for i in range(len(perfil.lista_favoritos)):
                                 if perfil.lista_favoritos[i] == c[0]:
                                     midia.id = c[0]
                                     midia.tipo = c[1]
                                     midia.titulo = c[2]
                                     midia.gênero = c[3]
                                     midia.ano_lançamento = c[4] 
                                     midia.classificação = c[5]
                                     midia.ExibirInfo()
                         
                         C.close()
                         escolha_midia = menu_Mídia()
                         
                    elif escolha_midia == 4:
                        F = open('catalogo.csv')
                        reader = csv.reader(F)
                        midia = Filme(None,None,None,None,None,None,None,None)
                        for i in reader:
                            if 'Filme' in i:
                                midia.id = i[0]
                                midia.tipo = i[1]
                                midia.titulo = i[2]
                                midia.gênero = i[3]
                                midia.ano_lançamento = i[4] 
                                midia.classificação = i[5]
                                midia.Diretor = i[7]
                                midia.Produtor = i[8]
                                midia.ExibirInfo()
                        F.close()
                        escolha_midia = menu_Mídia()
                        

                    elif escolha_midia == 5:
                        S = open('catalogo.csv')
                        reader = csv.reader(S)
                        midia = Série(None,None,None,None,None,None,None)
                        for i in reader:
                            if 'Serie' in i:
                                midia.id = i[0]
                                midia.tipo = i[1]
                                midia.titulo = i[2]
                                midia.gênero = i[3]
                                midia.ano_lançamento = i[4] 
                                midia.classificação = i[5]
                                midia.temp = i[6]
                                midia.ExibirInfo()
                                E = open('episodios.csv')
                                leitor = csv.reader(E)
                                for c in leitor:
                                    if midia.titulo in c:
                                        midia.episódios.append(c[2])
                                        print(midia.episódios)
                                        temporada = c[3],
                                        
                                        print(temporada)
                                
                                for l in range(len(midia.episódios)):
                                    print('[TEMPORADA] - ',temporada ,'\n[Episódio] - ',midia.episódios[l])
                        S.close()
                        E.close()
                        escolha_midia = menu_Mídia()
                        
                    elif escolha_midia == 6:
                        D = open('catalogo.csv')
                        reader = csv.reader(D)
                        midia = Documentário(None,None,None,None,None,None,None)
                        for i in reader:
                            if 'Documentario' in i:
                                midia.id = i[0]
                                midia.tipo = i[1]
                                midia.titulo = i[2]
                                midia.gênero = i[3]
                                midia.ano_lançamento = i[4] 
                                midia.classificação = i[5]
                                midia.tema = i [9]
                                midia.ExibirInfo()
                        
                        D.close()
                        escolha_midia = menu_Mídia()
                        
                    elif escolha_midia == 7:
                        midias = []
                        A = open('catalogo.csv')
                        reader = csv.reader(A)
                        midia = Animação(None,None,None,None,None,None, None)
                        for i in reader:
                            if 'Animacao' in i:
                                midia.id = i[0]
                                midia.tipo = i[1]
                                midia.titulo = i[2]
                                midia.gênero = i[3]
                                midia.ano_lançamento = i[4] 
                                midia.classificação = i[5]
                                midia.estudio = i[10]
                                midia.ExibirInfo()
                        
                        A.close()
                        escolha_midia = menu_Mídia()
                        
                    elif escolha_midia == 8:
                        P = open('catalogo.csv')
                        reader = csv.reader(P)
                        midia = ProgramaTV(None,None,None,None,None,None)
                        for i in reader:
                            if 'Programa de Auditorio' in i:
                                midia.id = i[0]
                                midia.tipo = i[1]
                                midia.titulo = i[2]
                                midia.gênero = i[3]
                                midia.ano_lançamento = i[4] 
                                midia.classificação = i[5]
                                midia.ExibirInfo()
                        
                        P.close()
                        escolha_midia = menu_Mídia()
                        break
                    else:
                        print('opção inválida, favor digitar outro número.')
                        escolha_midia = menu_Mídia()
                        break
                escolha_perfil = menu_perfil()        
            elif escolha_perfil == 3:
                if len(usuario.lista_perfis) == 0:
                    print('Usuário não possui perfis')
                    escolha_perfil = menu_perfil()
                else:
                    print('[Editar perfil]')
                    novo_nome = input('Informe o novo nome do perfil: ')
                    nova_idade = int(input('informe a idade atualizada do usuário deste perfil:  '))

                    P = open('perfilpoo2.csv')
                    reader = csv.reader(P)
                    for i in reader:
                        if perfil.nome in i:        #erro na idade
                            i[1] = novo_nome  
                            i[2] = nova_idade
                            print(i)
                    P.close()
                    perfil.nome = novo_nome
                    perfil.idade = nova_idade
                    print('Perfil editado com sucesso!')
                    escolha_perfil = menu_perfil()
            elif escolha_perfil == 4:
                if len(usuario.lista_perfis) < usuario.max_perfil:    
                    nome_novoperfil = input("Informe o nome do novo perfil: ")
                    idade_novoperfil = int(input('Informe a idade do usuário desse perfil: '))
                    perfil = Perfil(nome_novoperfil,idade_novoperfil)
                    usuario.addPerfil(perfil)
                    P = open('perfilpoo2.csv','a')
                    writer = csv.writer(P)
                    writer.writerow([usuario.nome_de_usuário,nome_novoperfil, idade_novoperfil])
                    P.close()
                else:
                    print('Número máximo de perfis alcançado')
                escolha_perfil = menu_perfil()
            elif escolha_perfil == 5:
                print('[Escolha o perfil a ser excluído]')
                for i in range(len(usuario.lista_perfis)):
                    print(usuario.lista_perfis[i].nome)
            
                indice = int(input('Informe o índice do perfil: '))
                usuario.RemoverPerfil(indice)
                escolha_perfil = menu_perfil()
            else:
                print('opção inválida, favor digitar outro número.')
                escolha_perfil = menu_perfil()
                
        acessado = False
        escolha = menu_acesso()
print('Saindo da Uniflix...')  


#Série • número de temporadas.  
#• lista de episódios por
#temporada
#• exibirInformações (especialização)
#• listarEpisodios(nro temporada), que
#apresenta os episódios da temporada

#Filme 
#• Diretor(a)
#• Produtor(a)
#• exibirInformações (especialização)

#Documentário • Tema • exibirInformações (especialização)

#Animação • Estúdio • exibirInformações (especialização)

#Programa de
#TV
#• Número de episódios
#• Lista de episódios
#• exibirInformações (especialização)
#• listarEpisodios()
#
