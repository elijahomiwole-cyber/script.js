function updateDashboard() {
    const total = pickups.length;

    const today = new Date().toISOString().split("T")[0];

    const todayCount = pickups.filter(p => p.date === today).length;

    const completedCount = pickups.filter(p => p.status === "completed").length;

    const pendingCount = pickups.filter(p => p.status !== "completed").length;

    document.getElementById("totalPickups").textContent = total;
    document.getElementById("todayPickups").textContent = todayCount;
    document.getElementById("completedPickups").textContent = completedCount;
    document.getElementById("pendingPickups").textContent = pendingCount;
}

displayPickups();
displayFeedback();
updateDashboard();
