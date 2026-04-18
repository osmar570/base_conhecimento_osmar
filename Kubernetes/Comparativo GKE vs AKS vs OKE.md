# GKE vs AKS vs OKE: [[Kubernetes]] Gerenciado

Quando você usa Kubernetes na nuvem, você utiliza um serviço **Gerenciado**. Isso significa que o provedor de nuvem cuida do *Control Plane* (o "cérebro" do cluster) e você se preocupa apenas com os *Worker Nodes* e suas aplicações.

---

## 1. GKE (Google Kubernetes Engine)
O GKE é amplamente considerado o serviço de Kubernetes mais maduro e avançado do mercado, o que faz sentido, já que o Kubernetes nasceu dentro do Google.

*   **Diferencial:** Possui o melhor sistema de [[Autoscaling no Kubernetes|Autoscaling]] e a melhor integração com a rede global do Google.
*   **Modo Autopilot:** Uma exclusividade que gerencia toda a infraestrutura, inclusive os nós, cobrando apenas pelo que os Pods consomem.
*   **Ideal para:** Quem busca a experiência mais próxima do "padrão ouro" do Kubernetes e alta automação.

## 2. AKS (Azure Kubernetes Service)
O serviço da Microsoft Azure foca muito na integração com o ecossistema corporativo da Microsoft.

*   **Diferencial:** Integração nativa e profunda com o **Active Directory (Entra ID)** para segurança e permissões.
*   **Custo:** Oferece um "Free Tier" para o Control Plane (embora para alta disponibilidade profissional exista uma taxa de SLA).
*   **Ideal para:** Empresas que já utilizam Azure, Windows Containers ou que dependem fortemente de políticas de segurança baseadas em AD.

## 3. OKE (Oracle Container Engine for Kubernetes)
A solução da Oracle Cloud (OCI) tem ganhado muito destaque recentemente por seu custo-benefício e performance de hardware.

*   **Diferencial:** O custo de saída de dados (egress) é muito mais barato que nos concorrentes. Além disso, a Oracle oferece instâncias **ARM (Ampere)** com um preço extremamente competitivo.
*   **Foco em Dados:** Excelente para rodar bancos de dados Oracle ou workloads que exigem muito processamento e storage de baixa latência.
*   **Ideal para:** Quem busca o menor custo de infraestrutura e utiliza intensamente serviços de dados da Oracle.

---

## Tabela Comparativa

| Recurso | GKE (Google) | AKS (Azure) | OKE (Oracle) |
| :--- | :--- | :--- | :--- |
| **Facilidade de Uso** | Muito Alta | Alta | Média |
| **Automação** | Líder (Autopilot) | Alta | Média |
| **Custo de Rede** | Alto | Alto | Baixo (Muito competitivo) |
| **Integração** | Ecossistema Google/Cloud Native | Microsoft / Active Directory | Oracle Database / ERPs |
| **Upgrade de Versão** | Automático e suave | Manual/Semi-automático | Manual/Controlado |

---

## Qual escolher?

1.  **Escolha GKE** se você quer a ferramenta mais moderna, com menos trabalho manual de manutenção e as melhores funcionalidades de escalonamento.
2.  **Escolha AKS** se sua empresa é "puro Microsoft" e você precisa que o Kubernetes converse perfeitamente com suas contas de usuário e ferramentas de segurança da Azure.
3.  **Escolha OKE** se o seu foco principal é redução de custos de infraestrutura bruta ou se você precisa de alta performance para bancos de dados massivos.

---
*Links relacionados:*
- [[como iniciar (GKE)]]
- [[Gerenciamento de Nodes (GKE)]]
