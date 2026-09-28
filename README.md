const quizData = {
  1: {
    correct: 298,
    tolerance: 1,
    success: "Benar! 25°C = 298 K. Rumus konversi: K = °C + 273.",
    error: "Coba lagi. Ingat, untuk konversi °C ke Kelvin, tambahkan 273."
  },
  2: {
    correct: 168000,
    tolerance: 1000,
    success: "Benar! Q = m × c × ΔT = 2 × 4200 × 20 = 168.000 J.",
    error: "Perhatikan rumus kalor sensibel: Q = m × c × ΔT. ΔT = 45 - 25 = 20°C."
  },
  3: {
    correct: 168000,
    tolerance: 1000,
    success: "Benar! Q = m × L = 0,5 × 336.000 = 168.000 J.",
    error: "Gunakan rumus kalor laten: Q = m × L. Ingat, es melebur tanpa perubahan suhu."
  },
  4: {
    correct: 50,
    tolerance: 1,
    success: "Benar! Suhu akhir campuran adalah 50°C karena massa dan kalor jenis sama.",
    error: "Saat dua air dengan massa sama dan kalor jenis sama dicampur, suhu akhir adalah rata-rata: (80 + 20) / 2 = 50°C."
  }
};

const cards = document.querySelectorAll(".quiz-card");

cards.forEach((card) => {
  const button = card.querySelector(".check-btn");
  const input = card.querySelector(".answer-input");
  const feedback = card.querySelector(".feedback");
  const questionNumber = Number(card.dataset.question);

  button.addEventListener("click", () => {
    const value = Number(input.value);
    const target = quizData[questionNumber];

    if (input.value.trim() === "") {
      feedback.textContent = "Silakan masukkan jawaban terlebih dahulu.";
      feedback.className = "feedback error";
      return;
    }

    const diff = Math.abs(value - target.correct);

    if (diff <= target.tolerance) {
      feedback.textContent = target.success;
      feedback.className = "feedback success";
    } else {
      feedback.textContent = target.error;
      feedback.className = "feedback error";
    }
  });
});

const resetBtn = document.getElementById("resetBtn");
resetBtn.addEventListener("click", () => {
  cards.forEach((card) => {
    const input = card.querySelector(".answer-input");
    const feedback = card.querySelector(".feedback");
    input.value = "";
    feedback.textContent = "";
    feedback.className = "feedback";
  });
});
