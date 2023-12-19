@echo off
SETLOCAL ENABLEDELAYEDEXPANSION
color 11
chcp 65001 > nul
                                                                                                           
:menu
color 17
cls
echo                     ██╗   ██╗ █████╗ ██╗   ██╗██████╗ ██╗███████╗████████╗ ██████╗  ██████╗ ██╗     
echo                     ██║   ██║██╔══██╗██║   ██║██╔══██╗██║██╔════╝╚══██╔══╝██╔═══██╗██╔═══██╗██║     
echo                     ██║   ██║███████║██║   ██║██████╔╝██║███████╗   ██║   ██║   ██║██║   ██║██║     
echo                     ╚██╗ ██╔╝██╔══██║╚██╗ ██╔╝██╔══██╗██║╚════██║   ██║   ██║   ██║██║   ██║██║     
echo                      ╚████╔╝ ██║  ██║ ╚████╔╝ ██║  ██║██║███████║   ██║   ╚██████╔╝╚██████╔╝███████╗
echo                       ╚═══╝  ╚═╝  ╚═╝  ╚═══╝  ╚═╝  ╚═╝╚═╝╚══════╝   ╚═╝    ╚═════╝  ╚═════╝ ╚══════╝
echo VavrisTOOL 1.0 hackmenu   
echo ------------------------------------------------------------------------------------------------------------------------ 


echo Vyberte možnost:
echo 1. Práce s uživateli
echo 2. Práce se skupinami
echo 3. Práce se sítí
echo 4. Práce s disky
echo 5. Konec

set /p choice=Zadejte číslo volby: 

if "%choice%"=="1" goto user_menu
if "%choice%"=="2" goto group_menu
if "%choice%"=="3" goto network
if "%choice%"=="4" goto disk
if "%choice%"=="5" goto end

echo Neplatná volba. Zadejte číslo volby od 1 do 5.
goto menu

:user_menu
cls
color 2
echo Menu pro práci s uživateli:
echo 1. Vytvořit uživatele
echo 2. Smazat uživatele
echo 3. Vypsat všechny uživatele
echo 4. Přidat uživatele do skupiny
echo 5. Odebrat uživatele ze skupiny
echo 6. Zpět do hlavního menu

set /p user_choice=Zadejte číslo volby: 

if "%user_choice%"=="1" goto create_user
if "%user_choice%"=="2" goto delete_user
if "%user_choice%"=="3" goto show_all_users
if "%user_choice%"=="4" goto add_to_group
if "%user_choice%"=="5" goto remove_from_group
if "%user_choice%"=="6" goto menu

echo Neplatná volba. Zadejte číslo volby od 1 do 7.
goto user_menu

:create_user
echo Volba 1: Vytvořit uživatele
set /p username=Zadejte uživatelské jméno: 
set /p password=Zadejte heslo: 
net user %username% %password% /add
pause
goto user_menu

:delete_user
echo Volba 2: Smazat uživatele
set /p username=Zadejte uživatelské jméno, které chcete smazat: 
net user %username% /delete
pause
goto user_menu

:show_all_users
echo Volba 3: Vypsat všechny uživatele
net user
pause
goto user_menu

:add_to_group
echo Volba 4: Přidat uživatele do skupiny
set /p user="Zadejte uživatelské jméno, které chcete přidat: "
set /p group="Zadejte skupinu, do které chcete uživatele přidat: "

net localgroup %group% %user% /add

if %ERRORLEVEL% == 0 (
    echo Uživatel %user% byl úspěšně přidán do skupiny %group%.
) else (
    echo Nastala chyba při přidávání uživatele %user% do skupiny %group%.
)
pause
goto user_menu

:remove_from_group
echo Volba 5: Odebrat uživatele ze skupiny
@echo off
set /p user="Zadejte uživatelské jméno, které chcete odebrat: "
set /p group="Zadejte skupinu, ze které chcete uživatele odebrat: "

net localgroup %group% %user% /delete

if %ERRORLEVEL% == 0 (
    echo Uživatel %user% byl úspěšně odebrán ze skupiny %group%.
) else (
    echo Nastala chyba při odebírání uživatele %user% ze skupiny %group%.
)

pause
goto user_menu

:group_menu
cls
color 3
echo Menu pro práci se skupinami:
echo 1. Vytvořit skupinu
echo 2. Smazat skupinu
echo 3. Vypsat všechny skupiny
echo 4. Zpět do hlavního menu

set /p group_choice=Zadejte číslo volby: 

if "%group_choice%"=="1" goto create_group
if "%group_choice%"=="2" goto delete_group
if "%group_choice%"=="3" goto show_all_groups
if "%group_choice%"=="4" goto menu

echo Neplatná volba. Zadejte číslo volby od 1 do 4.

goto group_menu

:create_group
set /p groupName="Zadejte název nové skupiny: "

net localgroup %groupName% /add

if %ERRORLEVEL% == 0 (
    echo Skupina %groupName% byla úspěšně vytvořena.
) else (
    echo Nastala chyba při vytváření skupiny %groupName%.
)
pause
goto group_menu

:delete_group
set /p groupName="Zadejte název skupiny, kterou chcete smazat: "

net localgroup %groupName% /delete

if %ERRORLEVEL% == 0 (
    echo Skupina %groupName% byla úspěšně smazána.
) else (
    echo Nastala chyba při mazání skupiny %groupName%.
)
pause
goto group_menu

:show_all_groups
net localgroup
pause
goto group_menu

:end
echo Konec programu.
                                                                                                          
pause