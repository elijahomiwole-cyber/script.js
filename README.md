function updateDashboard() {
    const total = pickups.length;

    const today = new Date().toISOString().split("T")[0];

    const todayCount = pickups.filter(p => p.date === today).length;

    const completedCount = pickups.filter(p => p.status === "completed").length;

    const pendingCount = pickups.filter(p => p.status !== "completed").length;

    const totalElement = document.getElementById("totalPickups");
    const todayElement = document.getElementById("todayPickups");
    const completedElement = document.getElementById("completedPickups");
    const pendingElement = document.getElementById("pendingPickups");

    if (totalElement) totalElement.textContent = total;
    if (todayElement) todayElement.textContent = todayCount;
    if (completedElement) completedElement.textContent = completedCount;
    if (pendingElement) pendingElement.textContent = pendingCount;
}

displayPickups();
displayFeedback();
updateDashboard();

const searchInput = document.getElementById("search");

if (searchInput) {
    searchInput.addEventListener("keyup", function () {
        const searchText = this.value.toLowerCase();

        const cards = document.querySelectorAll("#pickupList .card");

        cards.forEach(card => {
            const text = card.textContent.toLowerCase();
            card.style.display = text.includes(searchText) ? "block" : "none";
        });
    });
}
