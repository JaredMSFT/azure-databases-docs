---
ms.service: azure-cosmos-db
ms.subservice: mongodb
ms.topic: include
ms.date: 08/23/2024
ms.custom: sfi-ropc-blocked
---
1. Find the *CONNECTION STRING* from the list of keys and connection strings for the account with the [``Get-AzCosmosDBAccountKey``](/powershell/module/az.cosmosdb/get-azcosmosdbaccountkey) cmdlet.

    ```azurepowershell-interactive
    $parameters = @{
        ResourceGroupName = $RESOURCE_GROUP_NAME
        Name = $ACCOUNT_NAME
        Type = "ConnectionStrings"
    }    
    Get-AzCosmosDBAccountKey @parameters |
        Select-Object -Property "Primary MongoDB Connection String"    
    ```

1. Record the *CONNECTION STRING* value. You'll use these credentials later.
