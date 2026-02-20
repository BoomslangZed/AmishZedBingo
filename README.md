<!DOCTYPE html>
<html>
<head>
  <title>ISH Bingo PDF Generator</title>
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

    button {
      padding: 15px 30px;
      font-size: 18px;
      cursor: pointer;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 5px;
    }

    button:hover {
      background-color: #45a049;
    }
  </style>
</head>
<body>

<h1>🎉 ISH Bingo PDF Generator</h1>

<button onclick="generateAndDownloadPDF()">Generate Bingo PDF</button>

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

function generateRandomCard() {
  const shuffled = [...phrases].sort(() => 0.5 - Math.random());
  const selected = shuffled.slice(0, 24);
  selected.splice(12, 0, "FREE"); // FREE space in center
  return selected;
}

function generateAndDownloadPDF() {
  const card = generateRandomCard();
  const doc = new jsPDF();
  const pageWidth = doc.internal.pageSize.getWidth();

  // Title
  doc.setFontSize(22);
  doc.text("ISH BINGO", pageWidth / 2, 20, { align: "center" });

  const startX = 20;
  const startY = 40;
  const cellSize = 30;

  doc.setFontSize(8);

  // Draw grid and fill cells
  for (let row = 0; row < 5; row++) {
    for (let col = 0; col < 5; col++) {
      const x = startX + col * cellSize;
      const y = startY + row * cellSize;
      const text = card[row * 5 + col];

      doc.rect(x, y, cellSize, cellSize); // cell border

      // split text if too long
      const splitText = doc.splitTextToSize(text, cellSize - 4);
      doc.text(splitText, x + cellSize / 2, y + 8, {
        align: "center",
        maxWidth: cellSize - 4
      });
    }
  }

  doc.save("ish_bingo_card.pdf");
}
</script>

</body>
</html>
