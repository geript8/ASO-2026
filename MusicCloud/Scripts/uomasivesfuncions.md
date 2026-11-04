function New-DepartamentsOU {
    param(
        [Parameter(Mandatory=$true)]
        [string[]]$departaments,

        [Parameter(Mandatory=$false)]
        [string]$rutaPare = "OU=MusicCloud,DC=Musiccloud,DC=local"
    )

    try {
        $null = Get-ADObject -Identity $rutaPare -ErrorAction Stop
    } 
    catch {
        Write-Host "No existeix la ruta pare '$rutaPare'." -ForegroundColor Red
        return
    }

    foreach ($dep in $departaments) {
        try {
            $null = Get-ADOrganizationalUnit -Identity "OU=$dep,$rutaPare" -ErrorAction Stop
            Write-Host "El departament '$dep' ja existeix a '$rutaPare'." -ForegroundColor Yellow
        } 
        catch {
            New-ADOrganizationalUnit -Name $dep -Path $rutaPare
            Write-Host "S'ha creat el departament '$dep' dins de '$rutaPare'." -ForegroundColor Green
        }
    }
}

try {
    $null = Get-ADOrganizationalUnit -Identity "OU=MusicCloud,DC=Musiccloud,DC=local" -ErrorAction Stop
} catch {
    New-ADOrganizationalUnit -Name "MusicCloud" -Path "DC=Musiccloud,DC=local"
    Write-Host "S'ha creat la UO principal MusicCloud." -ForegroundColor Cyan
}

New-DepartamentsOU -departaments @("Usuaris", "Equips", "Grups") -rutaPare "OU=MusicCloud,DC=Musiccloud,DC=local"
New-DepartamentsOU -departaments @("Administracio", "Comercial", "Desenvolupament", "Sistemes", "Direccio") -rutaPare "OU=Usuaris,OU=MusicCloud,DC=Musiccloud,DC=local"
New-DepartamentsOU -departaments @("Clients", "Servidors") -rutaPare "OU=Equips,OU=MusicCloud,DC=Musiccloud,DC=local"