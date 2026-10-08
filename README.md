# 3d-wave-animation
Animated 3D sinusoidal wave surface plot in Python


import matplotlib.pyplot as plt
import numpy as np
from matplotlib.animation import ArtistAnimation

  # 1. Создаем графическое окно (фигуру) заданного размера (10 на 6 дюймов)
  # 1. Create a figure (window) with a specific size (10 by 6 inches)
fig = plt.figure(figsize=(10, 6))
  # 2. Добавляем на фигуру трехмерные (3D) оси для рисования объемных графиков
  # 2. Add 3D axes to the figure for drawing three-dimensional plots
ax_3d = fig.add_subplot(projection='3d')

  # 3. Генерируем одномерные массивы координат по X и Y от -2π до 2π с шагом 0.2
  # 3. Generate 1D coordinate arrays for X and Y from -2π to 2π with a step of 0.2
x = np.arange(-2*np.pi, 2*np.pi, 0.2) 
y = np.arange(-2*np.pi, 2*np.pi, 0.2) 
  # 4. Создаем двумерные сетки координат (матрицы) на основе векторов x и y
  # 4. Create 2D coordinate grids (matrices) based on the x and y vectors
xgrid, ygrid = np.meshgrid(x, y)

  # 5. Задаем массив фазовых сдвигов от 0 до 2π. Каждый шаг — отдельный кадр.
  # 5. Define an array of phase shifts from 0 to 2π. Each step represents a frame.
phasa = np.arange(0, 2*np.pi, 0.2) 
  # 6. Инициализируем пустой список для хранения объектов кадров
  # 6. Initialize an empty list to store the frame objects
frames = []

  # 7. Цикл по всем значениям фазы для генерации кадров
  # 7. Loop through all phase values to generate the animation frames
for p in phasa:
    # Вычисляем матрицу высот Z с учетом текущего сдвига фазы `p`
    # Calculate the Z-height matrix taking the current phase shift `p` into account
    zgrid = np.sin(xgrid + p) * np.sin(ygrid) / (xgrid * ygrid) \
    
    # Строим 3D-поверхность для текущего кадра с палитрой 'winter'
    # Plot the 3D surface for the current frame using the 'winter' colormap
  surf = ax_3d.plot_surface(xgrid, ygrid, zgrid, cmap='winter')
    # Добавляем поверхность в список. ArtistAnimation требует кадры в виде списков.
    # Append the surface to the list. ArtistAnimation requires frames as lists.
  frames.append([surf])

  # 8. Создаем объект анимации на основе подготовленного списка кадров `frames`
  # 8. Create the animation object based on the prepared `frames` list
  # (interval=50 ms delay, blit=False disables optimization, repeat=True loops it)
animation = ArtistAnimation(
    fig, 
    frames, 
    interval=50, 
    blit=False, 
    repeat=True
)
  # 9. Отображаем окно с интерактивным графиком и запущенной анимацией
  # 9. Display the window with the interactive plot and running animation
plt.show()



