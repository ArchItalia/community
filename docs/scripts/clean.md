🇬🇧 [English](#eng) - 🇮🇹 [Italian](#ita)


# ita

🇮🇹 Creare un comando semplificato `$ clean`  per personalizzare la pulizia del sistema.

![image](https://github.com/ArchItalia/site/assets/117321045/fff913e9-f5bb-40b6-bfec-7e0e78620bf2)




`$ sudo vim /usr/bin/clean`

<br>

```
#!/bin/bash

echo -e "\e[33mVerifica dei pacchetti e delle dipendenze non più necessarie..\e[0m"

if pacman -Qdt &> /dev/null; then
    echo  "Eliminazione dei pacchetti e delle dipendenze non più necessarie.."
    pacman -Qdt | awk '{print $1}' | sudo pacman -Rs -
else
    echo  "Non ci sono pacchetti da eliminare."
fi

echo -e "\e[33mVerifica pacchetti non più disponibili nei repositories dalla cache di pacman\e[0m"
sudo pacman -Scc 
echo ""
echo -e "\e[33mVerifica lo spazio occupato dalla directory ~/.cache\e[0m"
cache_size=$(du -sh ~/.cache | awk '{ print $1 }')
echo  "Lo spazio occupato dalla directory ~/.cache è di $cache_size."
echo ""
echo -e "\e[33mVerifica lo spazio occupato dal cestino\e[0m"
trash_size=$(du -sh ~/.local/share/Trash/files | awk '{ print $1 }')
echo "Lo spazio occupato dal cestino è di $trash_size."
echo ""
read -p "Vuoi svuotare il cestino e cancellare la directory ~/.cache? Rispondi con 'y' o 'n': " answer

if [ $answer = "y" ]; then
    # Svuota il cestino
    rm -rf ~/.local/share/Trash/files/*

    # Cancella la directory ~/.cache
    rm -rf ~/.cache/*

    echo  "Il cestino e la directory ~/.cache sono stati cancellati."
else
    echo  "Nessuna azione intrapresa."
fi

echo -e "\e[32mPulizia terminata!\e[0m"
```
<br>

`$ sudo chmod +x /usr/bin/clean`

<br><br>

# eng

🇬🇧 Create a simplified command `$ clean` to customize the system cleanup.

![image](https://github.com/ArchItalia/site/assets/117321045/ab9d9d0f-fe73-466a-8d51-86e6cac1e212)


`$ sudo vim /usr/bin/clean`

<br>

```
#!/bin/bash

echo -e "\e[33mChecking for unnecessary packages and dependencies..\e[0m"

if pacman -Qdt &> /dev/null; then
    echo -e "\e[33mRemoving unnecessary packages and dependencies..\e[0m"
    pacman -Qdt | awk '{print $1}' | sudo pacman -Rs -
else
    echo -e "\e[33mThere are no packages to remove.\e[0m"
fi

echo -e "\e[33mClearing pacman cache of packages no longer available in repositories\e[0m"
sudo pacman -Scc 
echo ""
echo -e "\e[33mChecking space occupied by ~/.cache directory\e[0m"
cache_size=$(du -sh ~/.cache | awk '{ print $1 }')
echo -e "\e[33mSpace occupied by ~/.cache directory is $cache_size.\e[0m"
echo ""
echo -e "\e[33mChecking space occupied by trash\e[0m"
trash_size=$(du -sh ~/.local/share/Trash/files | awk '{ print $1 }')
echo -e "\e[33mSpace occupied by trash is $trash_size.\e[0m"
echo ""
read -p "Do you want to empty the trash and  the ~/.cache directory? Answer with 'y' or 'n': " answer

if [ $answer = "y" ]; then
    # Empty the trash
    rm -rf ~/.local/share/Trash/files/*

    #  the ~/.cache directory
    rm -rf ~/.cache/*

    echo -e "\e[33mThe trash and ~/.cache directory have been d.\e[0m"
else
    echo -e "\e[33mNo action taken.\e[0m"
fi

echo -e "\e[32mCleanup completed!\e[0m"
```
<br>

`$ sudo chmod +x /usr/bin/clean`
