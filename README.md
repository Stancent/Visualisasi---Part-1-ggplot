# Visualisasi---Part-1-ggplot
Fundamental Visualisasi Data With R
library(dplyr)
library(ggplot2)

# Membaca dan memanipulasi data
tabel <- read.csv("https://storage.googleapis.com/dqlab-dataset/lo5_m01_mp01.csv") %>%
  mutate(Laki.laki = -Laki.laki) %>%
  arrange(desc(Kelompok.Usia))

# Membuat plot dengan ggplot2
plt <- ggplot(data = tabel, 
	aes(x = factor(tabel$Kelompok.Usia,
				   levels = tabel$Kelompok.Usia))) +
  geom_bar(aes(y = Laki.laki), 
		   stat = "identity", 
		   width = 0.8, 
		   fill = "blue") +
  geom_text(aes(x = Kelompok.Usia, 
				y = Laki.laki + 27, 
				label = abs(Laki.laki)), 
			colour = "white") +
  geom_bar(aes(y = Perempuan), 
		   stat = "identity", 
		   width = 0.8, 
		   fill = "orange") +
  geom_text(aes(x = Kelompok.Usia, 
				y = Perempuan - 27, 
				label = Perempuan), 
			colour = "white") +
  ylim(-550, 550) +
  coord_flip() +
  annotate("text", x = 0.5, y = -20, hjust = 1, 
		   label = "Laki-laki", 
		   colour = "blue") +
  annotate("text", x = 0.5, y = 20, hjust = 0, 
		   label = "Perempuan", 
		   colour = "orange") +
  labs(colour = "", x = "", y = "", 
	   title = "Perbandingan Jumlah Karyawan Laki-laki dan Perempuan\nBerdasarkan Kelompok Usia") +
  theme(axis.text = element_text(size = 12, face = "bold"),
        axis.text.x = element_blank(),
        axis.ticks = element_blank(),
        plot.title = element_text(hjust = 0, size = 16),
        panel.background = element_rect(fill = "white"),
        legend.position = "bottom")

# Mengatur ukuran tampilan plot
options(repr.plt.width = 10, repr.plt.height = 2)

# Menampilkan plot
plt

