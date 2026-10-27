
$nomOu = Read-Host "Introdueix el nom de la OU"

$rutaBase = "DC=Musiccloud,DC=local"

New-ADOrganizationalUnit -Name $nomOu -Path $rutaBase

Write-Host "S'ha creat correctament la OU: $nomOu"