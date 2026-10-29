param(
    [Parameter(Mandatory=$true)]
    [string]$nomOu,

    [Parameter(Mandatory=$false)]
    [string]$ruta = "DC=Musiccloud,DC=local"
)
try {
    $ou = Get-ADObject -Identity $ruta -ErrorAction Stop
} catch {
    Write-Host "No existeix la ruta '$ruta'"
    exit
}

try {
    $ou = Get-ADOrganizationalUnit -Identity "OU=$nomOu,$ruta" -ErrorAction Stop
} catch {
    $ou = $null
}

if (-not $ou) {
    New-ADOrganizationalUnit -Name $nomOu -Path $ruta
    Write-Host "S'ha creat la OU '$nomOu' a la ruta '$ruta'."
}