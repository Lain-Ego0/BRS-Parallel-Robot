# ROBOCON-BRS_robot | Black Rock Shooter (BRS)

[![English README](https://img.shields.io/badge/English-d9d9d9)](./README_EN.md)
[![Simplified Chinese README](https://img.shields.io/badge/简体中文-d9d9d9)](./README.md)

ROBOCON is a top-tier robotics competition that demands mechanical reliability, stable control electronics, and accurate perception.

This repository is an open-source snapshot of our 2025-season legged (quadruped) robot project, covering mechanical design, motion/force control, and ROS-based mapping/localization/navigation.

In the 2025 season, I led the full-stack R&D for Team 1 from mechanical modeling and motion control to autonomous navigation. By adopting a carbon-tube assembly chassis (inspired by plant protection drones), force control algorithms, and 3D LiDAR mapping & navigation, we achieved the following results.

## 2025 Results
- 2025 ROBOCON (Jiangyin) legged robot events (180+ teams):
  - Speed Race: 30th
  - Obstacle Race: 31st
  - Cross-Country Race: 34th
- National Second Prize in all three categories

## Highlights
- Carbon-fiber tube assembly structure and manufacturing approach
- Motion control and force control
- 3D LiDAR (Livox Mid-360) mapping/localization + ROS1 `move_base` navigation
- Host–slave architecture: ROS host ↔ STM32F427 slave (serial)

## Demos
<div align="center">
  <img src="./assets/models.png" width="90%" />
  <p>MATLAB: trajectory visualization and inverse-kinematics demo</p>
</div>

<div align="center">
  <img src="./assets/Portfolio-01-1.png" width="90%" />
</div>

<div align="center">
  <img src="./assets/Portfolio-01-2.png" width="90%" />
</div>

## System Architecture
<div align="center">
  <img src="./assets/Portfolio-01-3.png" width="90%" />
  <p>System architecture overview</p>
</div>

```mermaid
graph TD
    A[MID360 LiDAR publishes point cloud] --> B[FAST_LIO2 3D LiDAR mapping]
    B --> C[PCD point cloud → 2D grid map conversion]
    C --> D[Global relocalization]
    D --> E[ROS publishes initial pose]
    E --> F[move_base navigation (planning & control)]
    F --> G[Publish navigation goals]
    G --> H[Serial bridge subscribes to /Odometry and /cmd_vel]
```

## Calibration / Debug
<div align="center">
  <img src="./assets/image-20260111221812117.png" width="90%" />
  <p>Data reading in calibration mode</p>
</div>

## Repository Layout
| Path | Description |
| --- | --- |
| `1.Hardware/` | Mechanical design (SolidWorks parts/assemblies) and electronics project files (`.epro`) |
| `2.Software/Host/` | ROS host computer (SLAM/localization/navigation/communication), see [`2.Software/Host/README.md`](./2.Software/Host/README.md) |
| `2.Software/Slave/` | STM32F427 slave firmware (Keil uVision project: [`Lain_Iwakura.uvprojx`](<./2.Software/Slave/project/RVMDK(V5)/Lain_Iwakura.uvprojx>)) |
| `3.Document/` | Manuals and module datasheets (PDF) |
| `4.Picture/` | Competition videos (mp4) |
| `assets/` | Images used by READMEs |

## Quick Start (Where to look first)
- Host (ROS): [`2.Software/Host/README.md`](./2.Software/Host/README.md) (English) / [`2.Software/Host/README_CN.md`](./2.Software/Host/README_CN.md) (中文)
- Slave (Keil): open [`2.Software/Slave/project/RVMDK(V5)/Lain_Iwakura.uvprojx`](<./2.Software/Slave/project/RVMDK(V5)/Lain_Iwakura.uvprojx>)
- CAD (SolidWorks): open [`1.Hardware/models/总装配.SLDASM`](./1.Hardware/models/%E6%80%BB%E8%A3%85%E9%85%8D.SLDASM)

## Project Timeline
| Date | Milestone |
| --- | --- |
| 2024-08 | Project started |
| 2024-12 | First mechanical prototype completed |
| 2025-02 | First slave (embedded) version completed |
| 2025-04 | Host computer software completed |
| 2025-06 | Navigation feature completed |
| 2025-07 | Second slave version completed; competed in the same month |

## Changelog
| Date | Change |
| --- | --- |
| 2025-11 | Mechanical structure open-sourced |
| 2025-12 | Slave control software open-sourced |

## Acknowledgements
- Host navigation system reference: `NEXTE_Sentry_Nav` (66Lau): <https://github.com/66Lau/NEXTE_Sentry_Nav>
- Tutorials (Chinese):
  - <https://blog.csdn.net/weixin_52612260/article/details/134124028>
  - <https://blog.csdn.net/Hbutneymar/article/details/147161479>

## License
No `LICENSE` file is currently included in this repository. Please contact the author before reuse in papers or commercial projects.
