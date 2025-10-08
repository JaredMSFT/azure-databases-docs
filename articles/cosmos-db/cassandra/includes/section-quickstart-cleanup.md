---
ms.service: azure-cosmos-db
ms.subservice: apache-cassandra
ms.topic: include
ms.date: 07/21/2025
---

When you no longer need the account, remove the account from your Azure subscription by **deleting** the resource.

#### [Azure CLI](#tab/azure-cli)

```azurecli-interactive
az cosmosdb delete \
    --resource-group "<resource-group-name>" \
    --name "<account-name>"
```

#### [Azure portal](#tab/azure-portal)

1. Navigate to the existing **Azure Cosmos DB for Apache Cassandra** resource you created earlier in this guide.

1. On the resource's page, select **Delete** from the menu bar.

1. Follow the instructions in the confirmation dialog.

---
