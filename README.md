# Clean Dart
**Proposta de Arquitetura Limpa para o Dart/Flutter**

---

## **Camadas de uma Arquitetura Limpa**  
Baseado em **Robert C. Martin**, em *"Arquitetura Limpa: O Guia do Artesão para Estrutura e Design de Software"*.

Visão geral das camadas principais de uma arquitetura limpa:

1. **Regras de Negócio do Domínio**
2. **Regras de Negócio da Aplicação**
3. **Adaptadores de Interface**
4. **Frameworks & Drivers (Externos)**


<img src="https://github.com/user-attachments/assets/b20ac17d-a439-43db-bc24-52f0567445d7" alt="image" width="700">

---

### **Regras de Negócio do Domínio**
As regras de negócio cruciais para a aplicação, representadas por modelos de dados chamados **"Entidades"**. Essa camada contém as regras mais sensíveis de um sistema, por isso está no topo das camadas.  
Uma **Entidade** deve ser pura, ou seja, não deve conhecer nenhuma outra camada, mas é conhecida pelas camadas inferiores.

### **Regras de Negócio da Aplicação**
Regras executadas pelo sistema. Aqui temos os **Casos de Uso**, que representam ações do usuário na aplicação.  
**Casos de Uso** conhecem apenas as **Entidades**, sem conhecer implementações de camadas inferiores. Se precisarem de acesso a uma camada superior, isso deve ser feito através de **contratos (interfaces)**, conforme o **Princípio de Inversão de Dependências (SOLID)**.  

### **Adaptadores de Interface**
Esta camada é responsável por **converter dados externos** em formatos que atendam aos contratos definidos nas Regras de Negócio.  

### **Frameworks & Drivers**
Esta camada é a mais suscetível a mudanças. Com uma boa aplicação de arquitetura limpa, **trocar tecnologias** como APIs ou interfaces gráficas será seguro e não afetará as Regras de Negócio.

---

# **Clean Dart**

**Uma Proposta Aplicada ao Flutter**  
Aqui está como uma arquitetura limpa pode ser aplicada ao Flutter, utilizando o conceito de **Arquitetura Modular** e mantendo o foco nas regras de negócio do **Domínio da Aplicação**.

<img src="https://github.com/user-attachments/assets/f914d67c-a5e8-4dcc-8567-69df40225159" alt="image" width="700">

As camadas principais da arquitetura são:

1. **Presentation**
2. **Domain**
3. **Infrastructure (Infra)**
4. **External**

<img src="https://github.com/user-attachments/assets/0de4f307-ec89-4ec0-9b8f-b03772065cfb" alt="image" width="700">

### **Presentation**
A camada **Presentation** é responsável por **Widgets, Pages e Gerência de Estado** no Flutter. Ela lida diretamente com as interações do usuário.

### **Domain**
A camada **Domain** contém as **Entidades** e **Casos de Uso**.  
- **Entidades**: São objetos simples com regras de validação de dados (por exemplo, `ValueObjects`).  
- **Casos de Uso**: Executam a lógica de negócio, acessando camadas externas apenas por meio de contratos (interfaces).  
Não deve haver implementações de **Repositories** ou **Services** dentro do **Domain** — apenas os contratos de interface.

### **Infrastructure (Infra)**
Implementa as interfaces definidas no **Domain** e adapta dados externos para cumprir os contratos.  
Aqui podemos ter a implementação de **Repositories**, **Services**, **DataSources** (para acesso externo), e **Drivers** (para comunicação com hardware).

### **External**
A camada **External** contém tudo que pode ser alterado sem a intervenção do programador.  
No Flutter, por exemplo, o **SharedPreferences** pode ser substituído pelo **Hive** sem impactar o restante da arquitetura. Essa camada lida apenas com **dados externos** e **hardware**.

---

Essa proposta de arquitetura visa desacoplar as camadas externas e garantir a preservação das Regras de Negócio, facilitando manutenções e evolução do sistema.
