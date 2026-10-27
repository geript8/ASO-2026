$nomOu = "Musiccloud"

New-ADOrganizationalUnit -Name $nomOu -Path "DC=Musiccloud,DC=local"

Write-Host "S'ha creat correctament la OU: $nomOu"