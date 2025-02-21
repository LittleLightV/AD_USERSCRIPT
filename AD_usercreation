#Define the path to the CVS file
$csvPath = "C:\Users\jane_admin\Desktop\AD_User_Import.csv"

#Import The Data
$users = Import-Csv -Path $csvPath


#Review Data
$users | Format-Table -Property FirstName, LastName, Username, Password, OU, Department

#Ask for confirmation
$confirmation = Read-Host "Do you want to create these user accounts? (Y/N)"
if ($confirmation -eq "Y") {
    foreach ($user in $users) {
        # Creat AD User account
        New-ADUser -SamAccountName $user.Username `
                   -Name "$($user.FirstName) $($user.LastName)" `
                   -GivenName $user.FirstName `
                   -SurName $user.LastName `
                   -DisplayName "$($user.FirstName) $($user.LastName)" `
                   -Department $user.Department `
                   -PasswordNeverExpires $true `
                   -AccountPassword (ConvertTo-SecureString "Password1" -AsPlainText -Force) `
                   -Enabled $true `
                   -Path $user.OU
    }
    Write-Host "User accounts created successfully!"
    } else {
    Write-Host "User creation cancelled."
    }
