# GTA DayZ Brasil — primeira inicialização no Windows

Este guia prepara um ambiente **local de testes**. A GameMode ainda não foi compilada/testada neste computador.

## 1. Dependências

- Windows com XAMPP instalado e MySQL/MariaDB ativo.
- Banco de dados local chamado `dayz`, criado no phpMyAdmin.
- Pacote **SA-MP 0.3.7 Windows Server** (inclui `samp-server.exe` e as ferramentas de compilação Pawn). Verifique a origem do download antes de executar.
- Arquivos desta pasta `gamemode/`, preservando sua estrutura de diretórios e plugins.

## 2. Configuração inicial da GameMode

Em `gamemodes/dayz.pwn`, as definições iniciais são:

```pawn
#define mysql_host "127.0.0.1"
#define mysql_user "root"
#define mysql_password ""
#define mysql_database "dayz"
#define MAX_ZOMBIES 50
```

**Importante:** usuário `root` sem senha serve somente para teste local, se o XAMPP estiver assim configurado. Não exponha o MySQL à internet e não envie senhas pessoais para o GitHub.

O arquivo `server.cfg` está configurado para 10 jogadores, `maxnpc 50` e porta 7777. Substitua a senha `rcon_password` por uma senha forte **na cópia local** antes de iniciar; não publique essa senha.

## 3. Montar a pasta do servidor

1. Extraia o pacote SA-MP 0.3.7 Server numa pasta dedicada, como `C:\GTA-DayZ-Servidor`.
2. Copie o conteúdo de `gamemode/` para essa pasta, **mesclando** `gamemodes`, `pawno`, `plugins` e `scriptfiles`, e usando `server.cfg` deste projeto.
3. Confirme que existem `samp-server.exe`, `server.cfg`, `gamemodes\dayz.pwn` e os arquivos `.dll` indicados no `server.cfg`.

## 4. Compilar

1. Abra `gamemodes\dayz.pwn` no editor Pawn incluído no pacote, ou use o compilador `pawncc` com o diretório `pawno\include` configurado.
2. Compile e confira os erros e avisos. **Não presuma que a compilação vai funcionar:** esta GameMode é antiga e usa includes/plugins específicos.
3. O resultado esperado é `gamemodes\dayz.amx`. Sem ele, `samp-server.exe` não consegue carregar a GameMode.

## 5. Primeiro teste

1. Inicie MySQL no XAMPP.
2. Execute `samp-server.exe` na pasta do servidor.
3. Confira o console e `server_log.txt` para mensagens de conexão ao MySQL, carregamento de plugins e criação de tabelas.
4. No cliente SA-MP do mesmo notebook, conecte a `127.0.0.1:7777`.

## 6. Caso não funcione

- **Unknown gamemode**: confira se `gamemodes\dayz.amx` foi gerado.
- **Failed to load plugin**: verifique as versões do plugin, arquitetura 32 bits e dependências; plugins antigos podem ser incompatíveis com sistemas atuais.
- **Falha de MySQL**: confirme MySQL ativo, nome do banco, credenciais e compatibilidade da versão do plugin.
- **Falha de compilação**: guarde a mensagem exata de erro para corrigir a include ou a sintaxe correspondente.

## Estado atual

- [x] Banco local `dayz` criado pelo usuário.
- [x] Nome do banco e quantidade inicial de NPCs ajustados no repositório.
- [ ] Pacote SA-MP Server instalado no notebook.
- [ ] GameMode compilada e validada.
- [ ] Plugins e MySQL testados na inicialização.
- [ ] Textos da GameMode traduzidos para PT-BR.
- [ ] Inicialização automática do Windows configurada após o primeiro teste bem-sucedido.
