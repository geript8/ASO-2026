param(
    [Parameter(Mandatory=$true)]
    [string[]]$departaments,

    [Parameter(Mandatory=$false)]
    [string]$rutaPare = "OU=Equips,DC=Musiccloud,DC=local"
)

try {
    $ouPareObj = Get-ADObject -Identity $rutaPare -ErrorAction Stop
} catch {
    Write-Host "No existeix la ruta pare '$rutaPare'."
    exit
}

foreach ($dep in $departaments) {

    try {
        $ou = Get-ADOrganizationalUnit -Identity "OU=$dep,$rutaPare" -ErrorAction Stop
    } catch {
        $ou = $null
    }

    if (-not $ou) {
        New-ADOrganizationalUnit -Name $dep -Path $rutaPare
        Write-Host "S'ha creat el departament '$dep' dins de '$rutaPare'."
    } else {
        Write-Host "El departament '$dep' ja existeix a '$rutaPare'."
    }
}