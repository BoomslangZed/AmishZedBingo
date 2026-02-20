<!DOCTYPE html>
<html>
<head>
  <title>ISH Bingo PDF Generator</title>
  <!-- jsPDF library -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      margin-top: 50px;
    }

    h1 {
      margin-bottom: 30px;
    }

    /* Green button styling */
    button {
      padding: 15px 30px;
      font-size: 18px;
      cursor: pointer;
      background-color: #4CAF50; /* Green */
      color: white;
      border: none;
      border-radius: 5px;
    }

    button:hover {
      background-color: #45a049; /* Darker green on hover */
    }
  </style>
</head>
<body>

<h1>🎉 ISH Bingo PDF Generator</h1>

<!-- Updated button text -->
<button onclick="generateAndDownloadPDF()">CLICK TO GENERATE</button>

<script>
const { jsPDF } = window.jspdf;

const phrases = [
  'MORNING F',
  'ISH TALKS ABOUT RUN CLUB',
  'ISH STRIPS',
  'ISH MISSES A SHOT AGAINST A PLAYER',
  'ISH MISSES A SHOT AGAINST AN ANIMAL',
  'BABYZED PHOTO',
  'ISH PROMOTES NEW YT VIDEO',
  '"BURY"',
  'ISH GOES RED HUNGRY',
  'ISH TALKS ABOUT SKATEBOARDING',
  'ISH TALKS ABOUT COMCAST',
  'MY SUMMER CAR GETS MENTIONED',
  'ISH EATS A COSMIS CRISP APPLE',
  '"OI VEY"',
  'ISH GETS SCARED BY SCARE DONO',
  'SOMEONE MAKES ROBOT LADY GARGLE',
  'ISH MENTIONS GAME OF THRONES',
  '"I SAW A POST ON REDDIT"',
  'ISH SINGS BEAR NECESSETIES',
  'ISH MENTIONS PRAGUE',
  'ISH SAYS "PICKLE"',
  'ISH MENTIONS BILL',
  'ISH DIES',
  'DAYZ BUGS',
  'FERRO SHOT',
  '"I FOUND A _____ THERE"',
  'ISH BREAKS A LEG',
  'ORANGE TULUNE'
];

// Generate random Bingo card with FREE space
function generateRandomCard() {
  const shuffled = [...phrases].sort(() => Math.random() - 0.5);
  const selected = shuffled.slice(0, 24);
  selected.splice(12, 0, "FREE"); // FREE in the center
  return selected;
}

// Generate PDF and download
function generateAndDownloadPDF() {
  const card = generateRandomCard();
  const doc = new jsPDF();

  const pageWidth = doc.internal.pageSize.getWidth();

  // Title
  doc.setFontSize(22);
  doc.text("ISH BINGO", pageWidth / 2, 20, { align: "center" });

  const startX = 20;
  const startY = 40;
  const cellSize = 35;
  doc.setFontSize(9);

  for (let row = 0; row < 5; row++) {
    for (let col = 0; col < 5; col++) {
      const x = startX + col * cellSize;
      const y = startY + row * cellSize;
      const text = card[row * 5 + col];

      doc.rect(x, y, cellSize, cellSize); // Draw cell

      const splitText = doc.splitTextToSize(text, cellSize - 4);
      const textY = y + (cellSize / 2) - (splitText.length * 2);
      doc.text(splitText, x + cellSize / 2, textY + 4, { align: "center" });
    }
  }

  doc.save("ish_bingo_card.pdf");
}
</script>

</body>
</html>
