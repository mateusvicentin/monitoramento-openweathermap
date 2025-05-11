<h1 align="center">Monitoramento Climático em Tempo Real com Kafka, InfluxDB, Grafana e Telegram</h1> 
<p align="center"> <img src="https://miro.medium.com/v2/resize:fit:4800/format:webp/1*gQ9xpfF4nE7Jz-RCjWEmrA.png" alt="apresentação"> </p> 
<p>Este projeto tem como objetivo demonstrar uma arquitetura de ponta a ponta para coleta, armazenamento, visualização e notificação de dados meteorológicos em tempo real. Utilizando tecnologias modernas como Kafka, InfluxDB, Grafana e Telegram, o sistema permite obter dados de clima diretamente da API OpenWeatherMap e apresentá-los em dashboards interativos com alertas automatizados.</p>

<h2>Ferramentas:</h2>

<p>🌐 <strong>OpenWeatherMap API:</strong> Responsável por fornecer dados meteorológicos confiáveis, como temperatura, umidade, vento e descrição do clima atual da cidade de Votuporanga.</p>

<p>🐍 <strong>Python:</strong> Linguagem principal utilizada para programar dois serviços distintos:</p>
<ul>
  <li><strong>O producer</strong>, que coleta os dados da API e envia para o Kafka.</li>
  <li><strong>O consumer</strong>, que processa os dados recebidos e os armazena no InfluxDB, além de enviar para o Telegram.</li>
</ul>

<p>📡 <strong>Apache Kafka:</strong> Atua como um sistema de mensageria altamente performático e tolerante a falhas. Ele desacopla a coleta dos dados do seu processamento, garantindo confiabilidade na transmissão mesmo em cenários com falhas ou picos de carga.</p>

<p>🕒 <strong>InfluxDB:</strong> Um banco de dados de séries temporais otimizado para armazenar métricas que mudam com o tempo. Ele organiza os dados por tempo e permite consultas rápidas, agregações e análise de tendências.</p>

<p>📊 <strong>Grafana:</strong> Utilizado para criar dashboards dinâmicos e interativos, com gráficos atualizados automaticamente a cada minuto. Os dashboards oferecem uma visualização clara das condições climáticas em tempo real, com suporte a alertas visuais.</p>

<p>📲 <strong>Telegram:</strong> Integrado ao sistema para envio de notificações automáticas com os dados atuais do clima. Permite que os usuários acompanhem as condições diretamente pelo celular, sem precisar acessar o painel do Grafana.</p>

<h2>Funcionamento:</h2>

<p>
  A aplicação coleta dados meteorológicos da <strong><em>API</em></strong> do <strong><em>OpenWeatherMap</em></strong> e processa as informações de temperatura, umidade, velocidade do vento e clima atual. A arquitetura foi conteinerizada utilizando <strong><em>Docker</em></strong>, o que garante portabilidade e facilidade na orquestração dos serviços.
</p>

<p>
  Os serviços <em>Kafka</em>, <em>InfluxDB</em>, <em>Grafana</em> e <em>Zookeeper</em> foram encapsulados em containers e orquestrados por meio de um arquivo <code>docker-compose.yml</code>, possibilitando a execução integrada e automatizada de toda a solução.
</p>

<p align="center"> <img src="https://miro.medium.com/v2/format:webp/1*2aUPXTChw5gaGcyVqM3GVA.png" alt="apresentação"> </p> 
<p>
  O <strong>producer</strong> consulta a <strong>API</strong> a cada minuto e envia os dados coletados ao <strong>Kafka</strong>.
</p>

<p align="center"> <img src="https://miro.medium.com/v2/format:webp/1*UomW6INebqeVH-gQlU6ytA.png" alt="apresentação"> </p> 
<p>
  O <strong>consumer</strong> escuta esse tópico, processa a mensagem recebida, salva os dados no <strong>InfluxDB</strong> e envia uma notificação formatada ao <strong>Telegram</strong> com as informações mais recentes.
</p>

<p>
  Após os dados serem armazenados no <strong>InfluxDB</strong>, o <strong>Grafana</strong> é configurado para se conectar ao banco e montar um dashboard intuitivo com painéis de temperatura, umidade, vento e clima.
</p>

<p align="center"> <img src="https://miro.medium.com/v2/resize:fit:4800/format:webp/1*HvvBcVWXfVTv-MeysQIcNw.png" alt="apresentação"> </p> 
<p>
  Foi aplicado um tratamento de dados diretamente no <strong>Grafana</strong> para traduzir as descrições climáticas recebidas em inglês para o português. Embora essa conversão também pudesse ser realizada via script (por exemplo, no <strong>consumer</strong>), optei por implementá-la diretamente na interface do <strong>Grafana</strong> por praticidade e flexibilidade na visualização.
</p>

<p>
  Além do dashboard, o bot do <strong>Telegram</strong> fornece notificações diretas com os dados atuais, incluindo:
</p>

<ul>
  <li>Descrição do clima</li>
  <li>Temperatura</li>
  <li>Umidade</li>
  <li>Velocidade do vento</li>
</ul>

<p align="center"> <img src="https://miro.medium.com/v2/resize:fit:410/format:webp/1*9KLUUCl42yy5SUfxj8Tlwg.png" alt="apresentação"> </p> 

<p>
  Essa integração oferece praticidade e agilidade no monitoramento, principalmente para usuários que desejam ser informados mesmo fora da interface do <strong>Grafana</strong>.
</p>

<h3>Possibilidades de Expansão:</h3>
<p>
  Como melhoria futura, o sistema pode evoluir para identificar padrões nos dados meteorológicos, como a interpretação da velocidade do vento como indicativo de chuva iminente. Com base em tendências recentes e variações rápidas nos valores, seria possível prever mudanças no tempo e enviar alertas personalizados sobre possíveis chuvas nas próximas horas.
</p>

<p>
  Essa abordagem poderia incluir modelos preditivos simples baseados em regras ou, futuramente, até aplicar aprendizado de máquina sobre os dados coletados.
</p>


