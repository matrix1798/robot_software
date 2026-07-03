# Robot setup - instrukcja 

Repozytorium zawiera kod, instrukcję instalacji i uruchomienia programu sterującego [robotem do autonomicznego mapowania terenu](https://github.com/adasbl/Projekt-Grupowy-ID-656.git).

##  Wymagania wstępne

Zanim rozpoczniesz, upewnij się, że Twój komputer spełnia następujące wymagania:
* **System operacyjny:** Linux (zalecany [Ubuntu 22.04 LTS](https://releases.ubuntu.com/jammy/)).
* **Narzędzia:** Zainstalowany [system kontroli wersji `git`](instructions/git-instalation.md).
* **Połączenie sieciowe:** Komputer PC musi połączyć się z robotem poprzez wygenerowany hotspot drona 'jetson_hotspot' (hasło: `jetson_hotspot`).

---

##  Instrukcja instalacji krok po kroku

### Krok 1: Instalacja ROS 2 Humble
Jeśli nie masz jeszcze zainstalowanego systemu ROS 2, wykonaj pełną instalację w wersji **Humble** (Desktop) zgodnie z oficjalną dokumentacją:
 [Oficjalna instrukcja instalacji ROS 2 Humble (Ubuntu Debs)](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debs.html)

Po poprawnej instalacji upewnij się, że środowisko ładuje się poprawnie ([najlepiej dodać komendę `source /opt/ros/humble/setup.bash` do pliku `~/.bashrc`](instructions/ros2-environment-setup.md)).

### Krok 2: Instalacja wymaganych pakietów systemowych
Nasz system korzysta z zaawansowanych narzędzi ROS 2, które należy doinstalować. Uruchom w terminalu:

```bash
sudo apt update
sudo apt install ros-humble-navigation2 \
                 ros-humble-nav2-bringup \
                 ros-humble-slam-toolbox \
                 ros-humble-rviz2 \
                 ros-humble-teleop-twist-keyboard \
                 python3-colcon-common-extensions
```
### Krok 3: Budowa środowiska roboczego oraz pobranie wymaganych plików

Ponieważ pakiet eksploracji [m-explore](https://github.com/robo-friends/m-explore-ros2.git) nie jest oficjalnie dostępny w repozytoriach binarnych apt dla dystrybucji Humble, musimy pobrać jego port społecznościowy i zbudować go ręcznie ze źródeł wraz z Panelem Sterowania

```bash
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws/src

git clone https://github.com/matrix1798/robot_software.git

git clone https://github.com/robo-friends/m-explore-ros2.git

cd ~/ros2_ws
rosdep update
rosdep install --from-paths src --ignore-src -r -y

colcon build --symlink-install
```

### Krok 4: Konfiguracja sieci:
Aby Twój PC (Panel Sterowania) mógł bezkolizyjnie komunikować się z robotem (Jetsonem), oba urządzenia muszą pracować w tej samej domenie ROS. W tym projekcie używamy ID równego 30.

```bash
source /opt/ros/humble/setup.bash
source ~/ros2_ws/install/setup.bash
export ROS_DOMAIN_ID=30
```

### Krok 5: Uruchomienie systemu
Gdy wszystko jest już zainstalowane i zbudowane, uruchomienie Panelu Sterowania sprowadza się do jednej komendy.

```bash
python3 ~/ros2_ws/src/robot_software/control_panel.py
```
F
