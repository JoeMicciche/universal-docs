---
description: Textbox component for Universal Dashboard
---

# Textbox

A textbox lets users enter and edit text.

## Textbox

![](<../../../../.gitbook/assets/image (47).png>)

```powershell
New-UDTextbox -Label 'Standard' -Placeholder 'Textbox'
New-UDTextbox -Label 'Disabled' -Placeholder 'Textbox' -Disabled
New-UDTextbox -Label 'Textbox' -Value 'With value'
```

## Password Textbox

A password textbox will mask the input.

![](<../../../../.gitbook/assets/image (55).png>)

```powershell
New-UDTextbox -Label 'Password' -Type password
```

## Multiline

You can create a multiline textbox by using the `-Multiline` parameter. Pressing enter will add a new line. You can define the number of rows and the max number of rows using `-Rows` and `-RowsMax`.

```powershell
New-UDTextbox -Multiline -Rows 4 -RowsMax 10
```

## Interaction

### Retrieving a textbox value

You can use `Get-UDElement` to get the value of a textbox

```powershell
New-UDTextbox -Id 'txtExample' 
New-UDButton -OnClick {
    $Value = (Get-UDElement -Id 'txtExample').value 
    Show-UDToast -Message $Value
} -Text "Get textbox value"
```

### Setting the textbox value

```powershell
New-UDTextbox -Id 'txtExample' -Label 'Label' -Value 'Value'

New-UDButton -OnClick {

    Set-UDElement -Id 'txtExample' -Properties @{
        Value = "test123"
    }

} -Text "Get textbox value"
```

## Icons

You can set the icon of a textbox by using the `-Icon` parameter and the `New-UDIcon` cmdlet.

```powershell
New-UDTextbox -Id "ServerGroups" -Icon (New-UDIcon -Icon 'server') -Value "This is my server"
```

![](<../../../../.gitbook/assets/image (107).png>)

## Mask

You can define a text mask with a combination of strings and regular expressions. To specify a regular expression, use the JavaScript syntax in your string to start and finish the expression: `/\d/`.

This example creates a mask for US based phone numbers.

```powershell
New-UDTextbox -Mask @('+', '1', ' ', '(', '/[1-9]/', '/\d/', '/\d/', ')', ' ', '/\d/', '/\d/', '/\d/', '-', '/\d/', '/\d/', '/\d/', '/\d/')
```

![](<../../../../.gitbook/assets/image (172).png>)

## OnEnter

{% hint style="info" %}
Available in PowerShell Universal 2.9 or later.&#x20;
{% endhint %}

The `-OnEnter` event handler is executed when the user presses enter in the text field. It is useful for performing other actions, like clicking a button, on enter.&#x20;

```powershell
New-UDTextbox -OnEnter {
    Invoke-UDEndpoint -Id 'submit'
}

New-UDButton -Id 'submit' -OnClick {
    Show-UDToast -Message 'From Textbox'
}
```

## API

[New-UDTextbox](../../../../cmdlets/New-UDTextbox.txt)
