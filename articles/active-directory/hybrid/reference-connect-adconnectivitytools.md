---
title: 'Azure AD Connect: ADConnectivityTools PowerShell Reference | Microsoft Docs'
description: This document provides reference information for the ADConnectivityTools.psm1 PowerShell module.
author: billmath
manager: daveba
ms.service: active-directory
ms.workload: identity
ms.date: 10/19/2018
ms.subservice: hybrid
ms.author: billmath

---

# Azure AD Connect:  ADConnectivityTools PowerShell Reference
The following documentation provides reference information for the ADConnectivityTools.psm1 PowerShell Module that is included with Azure AD Connect.

## Confirm-DnsConnectivity

### SYNOPSIS
Detects local Dns issues.

### SYNTAX

```
Confirm-DnsConnectivity [-Forest] <String> [-DCs] <Array> [-ReturnResultAsPSObject] [<CommonParameters>]
```

### DESCRIPTION
Runs local Dns connectivity tests.
In order to configure the Active Directory connector, user must have both name resolution
for the forest he\she is attempting to connect to as well as in the domain controllers
associated to this forest.

### EXAMPLES

#### EXAMPLE 1
```
Confirm-DnsConnectivity -Forest "TEST.CONTOSO.COM" -DCs "MYDC1.CONTOSO.COM","MYDC2.CONTOSO.COM"
```

#### EXAMPLE 2
```
Confirm-DnsConnectivity -Forest "TEST.CONTOSO.COM"
```

### PARAMETERS

#### -Forest
Specifies the name of the forest to test against.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

#### -DCs
Specify DCs to test against.

```yaml
Type: Array
Parameter Sets: (All)
Aliases:

Required: True
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

#### -ReturnResultAsPSObject
Returns the result of this diagnosis in the form of a PSObject.
Not necessary during manual interaction with
this tool.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

#### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.
For more information, see about_CommonParameters (https://go.microsoft.com/fwlink/?LinkID=113216).

## Confirm-ForestExists

### SYNOPSIS
Determines if a specified forest exists.

### SYNTAX

```
Confirm-ForestExists [-Forest] <String> [<CommonParameters>]
```

### DESCRIPTION
Queries a DNS server for the IP addresses associated with a forest.

### EXAMPLES

#### EXAMPLE 1
```
Confirm-TargetsAreReachable -Forest "TEST.CONTOSO.COM"
```

### PARAMETERS

#### -Forest
Specifies the name of the forest to test against.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

#### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.
For more information, see about_CommonParameters (https://go.microsoft.com/fwlink/?LinkID=113216).

## Confirm-FunctionalLevel

### SYNOPSIS
Verifies AD forest functional level.

### SYNTAX

#### SamAccount
```
Confirm-FunctionalLevel -Forest <String> [-RunWithCurrentlyLoggedInUserCredentials] [<CommonParameters>]
```

#### ForestFQDN
```
Confirm-FunctionalLevel -ForestFQDN <Forest> [-RunWithCurrentlyLoggedInUserCredentials] [<CommonParameters>]
```

### DESCRIPTION
Verifies that the AD forest functional level is equal or more than a given MinAdForestVersion
(WindowsServer2003).
Account (Domain\Username) and Password may be requested.

### EXAMPLES

#### EXAMPLE 1
```
Confirm-FunctionalLevel -Forest "test.contoso.com"
```

#### EXAMPLE 2
```
Confirm-FunctionalLevel -Forest "test.contoso.com" -RunWithCurrentlyLoggedInUserCredentials -Verbose
```

#### EXAMPLE 3
```
Confirm-FunctionalLevel -ForestFQDN $ForestFQDN -RunWithCurrentlyLoggedInUserCredentials -Verbose
```

### PARAMETERS

#### -Forest
Target forest.
Default value is the Forest of the currently logged in user.

```yaml
Type: String
Parameter Sets: SamAccount
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

#### -ForestFQDN
Target ForestFQDN Object.

```yaml
Type: Forest
Parameter Sets: ForestFQDN
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

#### -RunWithCurrentlyLoggedInUserCredentials
The function will use the credentials of the user that is currently logged in the computer, rather than
requesting custom credentials from the user.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

#### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.
For more information, see about_CommonParameters (https://go.microsoft.com/fwlink/?LinkID=113216).

## Confirm-NetworkConnectivity

### SYNOPSIS
Detects local network connectivity issues.

### SYNTAX

```
Confirm-NetworkConnectivity [-DCs] <Array> [-SkipDnsPort] [-ReturnResultAsPSObject] [<CommonParameters>]
```

### DESCRIPTION
Runs local network connectivity tests.

For the local networking tests, AAD Connect must be able to communicate with the named
domain controllers on ports 53 (DNS), 88 (Kerberos) and 389 (LDAP) Most organizations run DNS
on their DCs, which is why this test is currently integrated.
Port 53 should be skipped
if another DNS server has been specified.

### EXAMPLES

#### EXAMPLE 1
```
Confirm-NetworkConnectivity -SkipDnsPort -DCs "MYDC1.CONTOSO.COM","MYDC2.CONTOSO.COM"
```

#### EXAMPLE 2
```
Confirm-NetworkConnectivity -DCs "MYDC1.CONTOSO.COM","MYDC2.CONTOSO.COM" -Verbose
```

### PARAMETERS

#### -DCs
Specify DCs to test against.

```yaml
Type: Array
Parameter Sets: (All)
Aliases:

Required: True
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

#### -SkipDnsPort
If user is not using DNS services provided by the AD Site / Logon DC, then he\she may want
to skip checking port 53. 
User must still be able to resolve _.ldap._tcp.\<forestfqdn\>
in order for the Active Directory Connector configuration to succeed.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

#### -ReturnResultAsPSObject
Returns the result of this diagnosis in the form of a PSObject.
Not necessary during manual interaction with
this tool.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

#### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.
For more information, see about_CommonParameters (https://go.microsoft.com/fwlink/?LinkID=113216).

## Confirm-TargetsAreReachable

### SYNOPSIS
Determines if a specified forest and its associated Domain Controllers are reachable.

### SYNTAX

```
Confirm-TargetsAreReachable [-Forest] <String> [-DCs] <Array> [<CommonParameters>]
```

### DESCRIPTION
Runs "ping" tests (whether a computer can reach a destination computer through the network
and/or the internet)

### EXAMPLES

#### EXAMPLE 1
```
Confirm-TargetsAreReachable -Forest "TEST.CONTOSO.COM" -DCs "MYDC1.CONTOSO.COM","MYDC2.CONTOSO.COM"
```

#### EXAMPLE 2
```
Confirm-TargetsAreReachable -Forest "TEST.CONTOSO.COM"
```

### PARAMETERS

#### -Forest
Specifies the name of the forest to test against.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

#### -DCs
Specify DCs to test against.

```yaml
Type: Array
Parameter Sets: (All)
Aliases:

Required: True
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

#### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.
For more information, see about_CommonParameters (https://go.microsoft.com/fwlink/?LinkID=113216).

## Confirm-ValidDomains

### SYNOPSIS
Validate that the domains in the obtained Forest FQDN are reachable

### SYNTAX

#### SamAccount
```
Confirm-ValidDomains [-Forest <String>] [-RunWithCurrentlyLoggedInUserCredentials] [<CommonParameters>]
```

#### ForestFQDN
```
Confirm-ValidDomains -ForestFQDN <Forest> [-RunWithCurrentlyLoggedInUserCredentials] [<CommonParameters>]
```

### DESCRIPTION
Validate that all of the domains in the obtained Forest FQDN are reachable by attempting
to retrieve DomainGuid and DomainDN.
Account (Domain\Username) and Password may be requested.

### EXAMPLES

#### EXAMPLE 1
```
Confirm-ValidDomains -Forest "test.contoso.com" -Verbose
```

#### EXAMPLE 2
```
Confirm-ValidDomains -Forest "test.contoso.com" -RunWithCurrentlyLoggedInUserCredentials -Verbose
```

#### EXAMPLE 3
```
Confirm-ValidDomains -ForestFQDN $ForestFQDN -RunWithCurrentlyLoggedInUserCredentials -Verbose
```

### PARAMETERS

#### -Forest
Target forest.

```yaml
Type: String
Parameter Sets: SamAccount
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

#### -ForestFQDN
Target ForestFQDN Object.

```yaml
Type: Forest
Parameter Sets: ForestFQDN
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

#### -RunWithCurrentlyLoggedInUserCredentials
The function will use the credentials of the user that is currently logged in the computer, rather than
requesting custom credentials from the user.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

#### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.
For more information, see about_CommonParameters (https://go.microsoft.com/fwlink/?LinkID=113216).

## Confirm-ValidEnterpriseAdminCredentials

### SYNOPSIS
Verifies if a user has Enterprise Admin credentials.

### SYNTAX

```
Confirm-ValidEnterpriseAdminCredentials [-RunWithCurrentlyLoggedInUserCredentials] [<CommonParameters>]
```

### DESCRIPTION
Searches if provided user has Enterprise Admin credentials.
Account (Domain\Username) and Password may
be requested.

### EXAMPLES

#### EXAMPLE 1
```
Confirm-ValidEnterpriseAdminCredentials -DomainName test.contoso.com -Verbose
```

#### EXAMPLE 2
```
Confirm-ValidEnterpriseAdminCredentials -RunWithCurrentlyLoggedInUserCredentials -Verbose
```

### PARAMETERS

#### -RunWithCurrentlyLoggedInUserCredentials
The function will use the credentials of the user that is currently logged in the computer, rather than
requesting custom credentials from the user.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

#### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.
For more information, see about_CommonParameters (https://go.microsoft.com/fwlink/?LinkID=113216).

## Get-DomainFQDNData

### SYNOPSIS
Retrieves a DomainFQDN out of an account and password combination.

### SYNTAX

```
Get-DomainFQDNData [[-DomainFQDNDataType] <String>] [-RunWithCurrentlyLoggedInUserCredentials]
 [-ReturnExceptionOnError] [<CommonParameters>]
```

### DESCRIPTION
Attempts to obtain a domainFQDN object out of provided credentials.
If the domainFQDN is valid,
a DomainFQDNName or RootDomainName will be returned, depending on the user's choice.
Account (Domain\Username)
and Password may be requested.

### EXAMPLES

#### EXAMPLE 1
```
Get-DomainFQDNData -DomainFQDNDataType DomainFQDNName -Verbose
```

#### EXAMPLE 2
```
Get-DomainFQDNData -DomainFQDNDataType RootDomainName -RunWithCurrentlyLoggedInUserCredentials
```

### PARAMETERS

#### -DomainFQDNDataType
Desired kind of data that will be retrieved.
Currently limited to "DomainFQDNName" or "RootDomainName".

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

#### -RunWithCurrentlyLoggedInUserCredentials
The function will use the credentials of the user that is currently logged in the computer, rather than
requesting custom credentials from the user.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

#### -ReturnExceptionOnError
Auxiliary parameter used by Start-NetworkConnectivityDiagnosisTools function

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

#### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.
For more information, see about_CommonParameters (https://go.microsoft.com/fwlink/?LinkID=113216).

## Get-ForestFQDN

### SYNOPSIS
Retrieves a ForestFQDN out of an account and password combination.

### SYNTAX

```
Get-ForestFQDN [-Forest] <String> [-RunWithCurrentlyLoggedInUserCredentials] [<CommonParameters>]
```

### DESCRIPTION
Attempts to obtain a ForestFQDN out of the provided credentials.
Account (Domain\Username) and Password
may be requested.

### EXAMPLES

#### EXAMPLE 1
```
Get-ForestFQDN -Forest CONTOSO.MICROSOFT.COM -Verbose
```

#### EXAMPLE 2
```
Get-ForestFQDN -Forest CONTOSO.MICROSOFT.COM -RunWithCurrentlyLoggedInUserCredentials -Verbose
```

### PARAMETERS

#### -Forest
Target forest.Default value is the Domain of the currently logged in user.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

#### -RunWithCurrentlyLoggedInUserCredentials
The function will use the credentials of the user that is currently logged in the computer, rather than
requesting custom credentials from the user.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

#### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.
For more information, see about_CommonParameters (https://go.microsoft.com/fwlink/?LinkID=113216).

## Start-ConnectivityValidation

### SYNOPSIS
Main function.

### SYNTAX

```
Start-ConnectivityValidation [-Forest] <String> [-AutoCreateConnectorAccount] <Boolean> [[-UserName] <String>]
 [<CommonParameters>]
```

### DESCRIPTION
Runs all the available mechanisms that verify AD credentials are valid.

### EXAMPLES

#### EXAMPLE 1
```
Start-ConnectivityValidation -Forest "test.contoso.com" -AutoCreateConnectorAccount $True -Verbose
```

### PARAMETERS

#### -Forest
Target forest.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

#### -AutoCreateConnectorAccount
For Custom-installations:
    Flag that is $True if the user chose "Create new AD account" on the AD Forest Account window of AADConnect's
    wizard.
$False if the user chose "Use existing AD account".
For Express-installations:
    The value of this variable must be $True for Express-installations.

```yaml
Type: Boolean
Parameter Sets: (All)
Aliases:

Required: True
Position: 2
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

#### -UserName
Parameter that pre-populates the Username field when user's credentials are requested.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 3
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

#### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.
For more information, see about_CommonParameters (https://go.microsoft.com/fwlink/?LinkID=113216).

## Start-NetworkConnectivityDiagnosisTools

### SYNOPSIS
Main function for network connectivity tests.

### SYNTAX

```
Start-NetworkConnectivityDiagnosisTools [[-Forest] <String>] [-Credentials] <PSCredential>
 [[-LogFileLocation] <String>] [[-DCs] <Array>] [-DisplayInformativeMessage] [-ReturnResultAsPSObject]
 [-ValidCredentials] [<CommonParameters>]
```

### DESCRIPTION
Runs local network connectivity tests.

### EXAMPLES

#### EXAMPLE 1
```
Start-NetworkConnectivityDiagnosisTools -Forest "TEST.CONTOSO.COM"
```

#### EXAMPLE 2
```
Start-NetworkConnectivityDiagnosisTools -Forest "TEST.CONTOSO.COM" -DCs "DC1.TEST.CONTOSO.COM", "DC2.TEST.CONTOSO.COM"
```

### PARAMETERS

#### -Forest
Specifies forest name to test against.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

#### -Credentials
The user name and password of the user that is running the test.
It requires the same level of permissions that is required to run the Azure AD Connect Wizard.

```yaml
Type: PSCredential
Parameter Sets: (All)
Aliases:

Required: True
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

#### -LogFileLocation
Specifies a the location of a log file that will contain the output of this function.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 3
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

#### -DCs
Specify DCs to test against.

```yaml
Type: Array
Parameter Sets: (All)
Aliases:

Required: False
Position: 4
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

#### -DisplayInformativeMessage
Flag that allows displaying a message about the purpose of this function.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

#### -ReturnResultAsPSObject
Returns the result of this diagnosis in the form of a PSObject.
Not necessary to specify during manual interaction with
this tool.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

#### -ValidCredentials
Indicates if the credentials the user typed are valid.
Not necessary to specify during manual interaction with
this tool.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

#### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.
For more information, see about_CommonParameters (https://go.microsoft.com/fwlink/?LinkID=113216).
