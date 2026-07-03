## Automatyczne ładowanie środowiska ROS 2

Po poprawnej instalacji ROS 2 warto skonfigurować terminal tak, aby środowisko ROS było ładowane automatycznie przy każdym jego uruchomieniu.

### 1. Dodaj konfigurację do pliku `~/.bashrc`

Uruchom w terminalu:

```bash
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
```

Polecenie dopisze do pliku `~/.bashrc` linię odpowiedzialną za automatyczne ładowanie środowiska ROS 2.

### 2. Załaduj zmiany

Aby zastosować zmiany bez ponownego uruchamiania terminala, wykonaj:

```bash
source ~/.bashrc
```

### 3. Sprawdź poprawność konfiguracji

Zweryfikuj, czy zmienne środowiskowe ROS zostały załadowane:

```bash
printenv | grep ROS
```

Przykładowy wynik:

```text
ROS_VERSION=2
ROS_DISTRO=humble
```

Możesz również sprawdzić dostępność polecenia `ros2`:

```bash
ros2
```

Jeżeli wyświetli się pomoc programu `ros2`, oznacza to, że środowisko zostało poprawnie skonfigurowane.

## Rozwiązywanie problemów

Jeżeli podczas wykonywania polecenia:

```bash
source ~/.bashrc
```

pojawi się komunikat:

```text
bash: /opt/ros/humble/setup.bash: No such file or directory
```

oznacza to, że ROS 2 Humble nie został poprawnie zainstalowany lub znajduje się w innej lokalizacji.

Możesz zweryfikować instalację poleceniem:

```bash
ls /opt/ros
```

Jeżeli katalog `humble` nie istnieje, wróć do kroku instalacji ROS 2.