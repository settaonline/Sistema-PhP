# CHECKLIST DE BOAS PRÁTICAS E SEGURANÇA

## 1. Segurança
1.1 Proteção contra SQL Injection: Todos os comandos SQL usam prepare/bind, evitando SQL Injection.
1.2 Escape de Output: Função e() (htmlspecialchars) está presente em todos os arquivos para saída HTML.
1.3 CSRF Token: Implementado nos principais formulários (cadastrar_cliente.php, cadastrar_os.php).
1.4 Validação de sessão/login: Uso consistente de require_login() e require_perfil().
1.5 Validação de permissões: Usuários só acessam recursos conforme perfil.
1.6 Validação de uploads: Em os_anexos.php, nomes de arquivos são sanitizados; diretório de uploads é criado com permissão restrita.
1.7 Hash seguro de senha: Uso de password_hash/password_verify (BCRYPT) para senhas.
1.8 Destruição segura da sessão: Implementada em logout.php.
1.9 Evita headers already sent: Usa ob_start em pontos críticos.
1.10 Charset seguro: SET NAMES utf8mb4 usado nas conexões.
1.11 Limite de tamanho em uploads: Recomenda-se validar também via PHP (ini_set, $_FILES).

## 2. Organização do Código
2.1 Funções utilitárias isoladas: Funções como e(), csrf_token(), etc.
2.2 Separação de responsabilidades: Autenticação, menu, dashboard, cadastro, API etc, cada em seu arquivo.
2.3 Uso de includes condicionais: Exemplo: header_menu.php.
2.4 Polyfill para compatibilidade PHP: Exemplo: str_contains no header_menu.php.
2.5 Estrutura de diretórios clara: public/, uploads/, Connections/, etc.
2.6 Uso de prepared statements nas queries.
2.7 Evita duplicação de código: Funções de mapeamento de colunas, validação, etc, reaproveitadas.

## 3. Usabilidade
3.1 Mensagens de erro/sucesso claras.
3.2 Redirecionamento robusto pós-formulário.
3.3 Autocomplete de clientes nos formulários de OS.
3.4 Campos obrigatórios sinalizados.
3.5 Paginação em listas grandes.
3.6 Filtros dinâmicos nas listas.
3.7 Dashboard com gráficos e KPIs.
3.8 Interface responsiva e moderna (Inter, FontAwesome, CSS customizado).

## 4. Sugestões de melhoria
### Segurança e robustez
4.1 Validação de tamanho e tipo de arquivo em uploads (os_anexos.php): Adicione validação PHP para tamanho máximo e tipos permitidos (exemplo: PDF, JPG, PNG).
4.2 Envio de senha por e-mail: Nunca implemente envio de senha em texto puro. Sempre gere link de redefinição.
4.3 Limitar tentativas de login: Considere implementar throttle/lockout após X tentativas para evitar brute force.
4.4 Log de ações administrativas: Recomenda-se registrar quem editou/excluiu usuários e anexos.
4.5 Proteção contra XSS em campos de texto grandes: Embora use e(), revise se algum campo pode exibir HTML malicioso.
4.6 Configurar diretório uploads/ para não executar scripts: Adicione .htaccess ou equivalente.
4.7 Utilizar HTTPS: Garanta que toda navegação e login aconteçam via HTTPS.

### Código e manutenção
4.8 Reaproveitamento de funções utilitárias: Centralize helpers como pick_col, get_pk, etc, em um único arquivo.
4.9 Padronizar nomes de variáveis: Por exemplo, $data, $conn, $pdo, $mysqli nos arquivos de conexão.
4.10 Documentação: Adicione README detalhado, instruções de instalação, e comentários nos pontos críticos.
4.11 Testes automatizados: Considere iniciar testes unitários para funções críticas (login, cadastro, API).
4.12 Controle de versão dos scripts SQL: Mantenha scripts de criação/alteração das tabelas no repositório.

### Interface
4.13 Acessibilidade: Adicione aria-label, contraste, navegação por teclado em formulários.
4.14 Campos de e-mail e outros: Se a tabela de cliente tiver campo de e-mail, inclua nos formulários.
4.15 Campo de busca avançada: Permitir filtros mais detalhados nas listas.

---

Seu sistema PHP está bem estruturado, seguro e organizado — já atende a maioria das boas práticas recomendadas para sistemas de cadastro e gestão. Se quiser implementar algum dos tópicos acima, peça sugestões ou código pronto!