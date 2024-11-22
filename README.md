Descrição do Projeto
O Smart Home Energy Management é uma solução web desenvolvida para monitorar, analisar e otimizar o consumo de energia elétrica em residências. Com foco em sustentabilidade, o sistema oferece insights e sugestões personalizadas, baseados em Inteligência Artificial Generativa (OpenAI), para ajudar os usuários a economizar energia e reduzir o impacto ambiental.
Funcionalidades
1.	Monitoramento de dispositivos:
a.	Listagem de dispositivos conectados.
b.	Status em tempo real (ativo/inativo).
c.	Consumo de energia individual.
2.	Controle de dispositivos:
a.	Habilitar/desabilitar dispositivos remotamente.
3.	Paginação:
a.	Exibe grandes quantidades de dispositivos em páginas para melhor navegação.
4.	Sugestões com IA (OpenAI):
a.	Sugestões personalizadas para economia de energia com base no consumo atual.
5.	Segurança:
a.	Autenticação e autorização com Spring Security.
b.	Perfis de usuário (USER, ADMIN) com permissões distintas.
6.	Mensageria com RabbitMQ:
a.	Comunicação assíncrona para otimizar notificações e tarefas de segundo plano.
7.	Persistência de Dados:
a.	Integração com MongoDB para armazenamento de dados de dispositivos.
8.	Boas práticas e validação:
a.	Validação de entradas com Bean Validation.
b.	Tratamento de exceções centralizado.
Tecnologias Utilizadas
•	Backend: Spring Boot (3.3.5)
•	Banco de Dados: MongoDB
•	Mensageria: RabbitMQ
•	Inteligência Artificial: OpenAI GPT-3.5 Turbo integrado via Spring AI
•	Linguagem de Programação: Java 17
•	Ferramentas de Build: Maven
•	Segurança: Spring Security com autenticação básica.
Como Executar o Projeto
Pré-requisitos
1.	Java 17 ou superior instalado.
2.	Maven configurado corretamente no PATH.
3.	MongoDB rodando localmente na porta 27017.
4.	RabbitMQ rodando localmente na porta 5672.
5.	Configuração de rede ativa para acesso à API OpenAI.
API Endpoints
Dispositivos
1.	Listar dispositivos (com paginação):
a.	GET /api/devices?page={page}&size={size}
b.	Descrição: Retorna a lista de dispositivos com paginação.
Exemplo:
Bash: curl -u user:user123 http://localhost:8080/api/devices?page=0&size=10

2.	Listar dispositivos por status (ativo/inativo):
•	GET /api/devices/status?status={true|false}&page={page}&size={size}
•	Descrição: Retorna os dispositivos filtrados por status.

Exemplo: bash: curl -u user:user123 http://localhost:8080/api/devices/status?status=true&page=0&size=5
Alternar status do dispositivo:
•	POST /api/devices/{id}/toggle
•	Descrição: Alterna o status (ativo/inativo) de um dispositivo. Requer permissão de ADMIN.
Exemplo: bash: curl -X POST -u admin:admin123 http://localhost:8080/api/devices/1/toggle

Criar um novo dispositivo:
•	POST /api/devices
•	Descrição: Adiciona um novo dispositivo ao sistema.
Exemplo: bash: curl -X POST -u admin:admin123 \
-H "Content-Type: application/json" \
-d '{"name":"Ar Condicionado","status":false,"consumption":1200}' \
http://localhost:8080/api/devices
Sugestões de Economia de Energia
1.	Gerar Sugestões:
a.	POST /api/devices/suggestions
b.	Descrição: Envia o consumo de energia e recebe sugestões práticas de economia.
Exemplo: bash: curl -X POST -u user:user123 \
-H "Content-Type: application/json" \
-d '{"consumption":200}' \
http://localhost:8080/api/devices/suggestions
Arquitetura do Projeto
Pacotes
•	model: Contém as classes de modelo do MongoDB.
•	repository: Gerencia a persistência de dados usando Spring Data MongoDB.
•	service: Contém a lógica de negócios.
•	controllers: Implementa os endpoints REST da API.
•	config: Configurações de segurança e integração.
•	dto: Objetos para transferência de dados.
Fluxo Principal
1.	O cliente (frontend ou ferramenta como Postman) faz uma requisição à API.
2.	O controlador (Controller) gerencia a entrada e direciona para o serviço (Service).
3.	O serviço processa a lógica de negócios e interage com o repositório (Repository).
4.	Resposta formatada é enviada de volta ao cliente.
Credenciais de Teste
•	Admin:
o	Username: admin
o	Password: admin123
•	User:
o	Username: user
o	Password: user123

Possíveis Melhorias
•	Adicionar interface gráfica (frontend) com React ou Angular.
•	Notificações em tempo real com WebSocket.
•	Configurar um serviço de deploy automático (Heroku, AWS, ou GCP).
•	Suporte para múltiplos usuários com autenticação OAuth.
