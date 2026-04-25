import matplotlib.pyplot as plt
import numpy as np

def plot_tetragonal(lattice_type='primitive', a=1.0, c=1.5):
    fig = plt.figure(figsize=(10, 8))
    ax = fig.add_subplot(111, projection='3d')

    # Koordinat 8 sudut sel satuan
    corners = np.array([
        [0, 0, 0], [a, 0, 0], [a, a, 0], [0, a, 0],
        [0, 0, c], [a, 0, c], [a, a, c], [0, a, c]
    ])

    # Menggambar rusuk/bingkai kristal
    edges = [
        [0, 1], [1, 2], [2, 3], [3, 0], # Bawah
        [4, 5], [5, 6], [6, 7], [7, 4], # Atas
        [0, 4], [1, 5], [2, 6], [3, 7]  # Tiang tegak
    ]

    for edge in edges:
        ax.plot3D(*zip(corners[edge[0]], corners[edge[1]]), color="gray", linestyle='--')

    # Menentukan posisi atom berdasarkan tipe kisi
    atoms = corners.tolist()
    colors = ['blue'] * 8

    if lattice_type.lower() == 'body-centered':
        # Tambah satu atom di tengah (a/2, a/2, c/2)
        atoms.append([a/2, a/2, c/2])
        colors.append('red')
        title = "Sistem Kristal Tetragonal: Body-Centered (I)"
    else:
        title = "Sistem Kristal Tetragonal: Primitive (P)"

    atoms = np.array(atoms)
    ax.scatter(atoms[:,0], atoms[:,1], atoms[:,2], s=200, c=colors, edgecolors='black')

    ax.set_title(title, fontsize=15)
    ax.set_xlabel('Sumbu a')
    ax.set_ylabel('Sumbu b')
    ax.set_zlabel('Sumbu c')
    ax.set_box_aspect([a, a, c]) # Memastikan rasio visual sesuai parameter kisi
    plt.show()

# Jalankan visualisasi
# Ganti ke 'body-centered' untuk melihat tipe kedua
plot_tetragonal(lattice_type='primitive', a=1, c=1.8)
