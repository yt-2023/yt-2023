const words = ['MERCH', 'SHOP', 'BUY', 'SELL', 'DEAL', 'SALE', 'CART'];

const grid = document.getElementById('wordsearch');
const message = document.getElementById('message');
let selectedWord = '';

// Create word search grid
for (let i = 0; i < 64; i++) {
    const cell = document.createElement('div');
    cell.textContent = getRandomLetter();
    cell.addEventListener('click', () => {
        if (cell.classList.contains('selected')) {
            cell.classList.remove('selected');
            selectedWord = '';
        } else {
            clearSelection();
            cell.classList.add('selected');
            selectedWord = getSelectedWord();
        }
    });
    grid.appendChild(cell);
}

// Get random letter
function getRandomLetter() {
    return String.fromCharCode(65 + Math.floor(Math.random() * 26));
}

// Clear word selection
function clearSelection() {
    const selectedCells = document.querySelectorAll('.selected');
    selectedCells.forEach(cell => cell.classList.remove('selected'));
}

// Get selected word
function getSelectedWord() {
    const selectedCells = document.querySelectorAll('.selected');
    let word = '';
    selectedCells.forEach(cell => word += cell.textContent);
    return word;
}

// Check if selected word is correct
function checkWord() {
    if (selectedWord) {
        if (words.includes(selectedWord)) {
            message.textContent = `Congratulations! You found the word "${selectedWord}".`;
        } else {
            message.textContent = 'Sorry, the selected word is incorrect. Please try again.';
        }
    } else {
        message.textContent = 'Please select a word from the grid.';
    }
}
