---
 ms.service: azure-cosmos-db
 ms.topic: include
 ms.date: 08/23/2024
---
   
1. From the Azure portal menu or the home page, select **Create a resource**.

1. On the **New** page, search for and select **Azure Cosmos DB**.

1. On the **Azure Cosmos DB** page, select **Create**.

1. On the **API** page, under the **Cassandra** section, select **Create**.

   The API determines the type of account to create. Azure Cosmos DB provides five APIs: NoSQL for document databases, Gremlin for graph databases, MongoDB for document databases, Azure Table, and Cassandra. You must create a separate account for each API.

   Select **Cassandra** because in this tutorial you're creating a table that works with the API for Cassandra.

   To learn more about the API for Cassandra, see [What is Azure Cosmos DB for Apache Cassandra?](../cassandra/introduction.md).

1. On the **Create Azure Cosmos DB Account** page, enter the basic settings for the new Azure Cosmos DB account.

   |Setting|Value|Description |
   |---|---|---|
   | **Subscription**|Your subscription.|Select the Azure subscription that you want to use for this Azure Cosmos DB account. |
   | **Resource Group**|Create new.<br><br>Then enter the same name as **Account Name**.|Select **Create new**. Then enter a new resource group name for your account. For simplicity, use the same name as your Azure Cosmos DB account name. |
   | **Account Name**|Enter a unique name.|Enter a unique name to identify your Azure Cosmos DB account. Your account URI, `cassandra.cosmos.azure.com`, appended to your unique account name.<br><br>The account name can use only lowercase letters, numbers, and hyphens (-) and must be between 3 and 31 characters long.|
   |**Location**|The region closest to your users.|Select a geographic location to host your Azure Cosmos DB account. Use the location that's closest to your users to give them the fastest access to the data.|
   |**Capacity mode**|**Provisioned throughput** or **Serverless**.|Select **Provisioned throughput** to create an account in [Provisioned throughput](../set-throughput.md) mode. Select **Serverless** to create an account in [Serverless](../serverless.md) mode.|
   |**Apply Azure Cosmos DB free tier discount**|**Apply** or **Do not apply**.|With the Azure Cosmos DB free tier, you get the first 1,000 RU/s and 25 GB of storage for free in an account. Learn more about the [free tier](https://azure.microsoft.com/pricing/details/cosmos-db/).|
   |**Limit total account throughput**|Select to limit throughput of the account.|This option is useful if you want to limit the total throughput of the account to a specific value.|

   > [!NOTE]
   > You can have up to one free tier Azure Cosmos DB account per Azure subscription. You must opt in when you create the account. If you don't see the option to apply the free tier discount, another account in the subscription was enabled with the free tier.

   :::image type="content" source="./media/cosmos-db-create-dbaccount-cassandra/azure-cosmos-db-create-new-account.png" alt-text="The new account page for Azure Cosmos DB for Apache Cassandra":::

1. On the **Global Distribution** tab, configure the following details. Use the default values for this tutorial.

   |Setting|Value|Description |
   |---|---|---|
   |**Geo-Redundancy**|Disable|Enable or disable global distribution on your account by pairing your region with a pair region. You can add more regions to your account later.|
   |**Multi-region Writes**|Disable|With the multiregion writes capability, you can take advantage of the provisioned throughput for your databases and containers across the globe.|
   |**Availability Zones**|Disable|Availability zones are isolated locations within an Azure region. Each zone is made up of one or more datacenters equipped with independent power, cooling, and networking.|

   The following options aren't available if you select **Serverless** as the **Capacity mode**:
   - **Apply Free Tier Discount**
   - **Geo-redundancy**
   - **Multi-region Writes**

1. Optionally, you can configure other details on the following tabs:

   * **Networking**: Configure [access from a virtual network](../how-to-configure-vnet-service-endpoint.md).
   * **Backup Policy**: Configure either [periodic](../periodic-backup-restore-introduction.md) or [continuous](../provision-account-continuous-backup.md) backup policy.
   * **Encryption**: Use either a service-managed key or a [customer-managed key](../how-to-setup-cmk.md#create-a-new-azure-cosmos-account).
   * **Tags**: Tags are name/value pairs that you can use to categorize resources and view consolidated billing by applying the same tag to multiple resources and resource groups.

1. Select **Review + create**.

1. Review the account settings, and then select **Create**. It takes a few minutes to create the account. Wait for the portal page to display **Your deployment is complete**.

   :::image type="content" source="~/reusable-content/ce-skilling/azure/media/cosmos-db/azure-cosmos-db-account-created.png" alt-text="Screenshot that shows the Azure portal Notifications pane.":::

1. Select **Go to resource** to go to the Azure Cosmos DB account page.
