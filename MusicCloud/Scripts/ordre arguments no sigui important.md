param(
    [string]$nomOu,
    [string]$rutaBase = "DC=Musiccloud,DC=local"
)

# Creem la OU amb els arguments rebuts
New-ADOrganizationalUnit -Name $nomOu -Path $rutaBase

Write-Host "S'ha creat correctament la OU '$nomOu' a la ruta '$rutaBase'."