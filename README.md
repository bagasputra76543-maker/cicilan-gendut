<script>
const nominal = 200000;
const total = nominal * document.querySelectorAll("#data tr").length;

document.getElementById("total").textContent = total.toLocaleString("id-ID");

let status = JSON.parse(localStorage.getItem("statusCicilan")) || [];
let sudah = 0;

const tombol = document.querySelectorAll("#data button");

tombol.forEach((btn, index) => {

    if (status[index]) {
        btn.innerHTML = "✔ Lunas";
        btn.closest("tr").classList.add("lunas");
        sudah += nominal;
    }

    btn.onclick = function () {

        const baris = this.closest("tr");

        if (status[index]) {
            status[index] = false;
            this.innerHTML = "Belum";
            baris.classList.remove("lunas");
            sudah -= nominal;
        } else {
            status[index] = true;
            this.innerHTML = "✔ Lunas";
            baris.classList.add("lunas");
            sudah += nominal;
        }

        localStorage.setItem("statusCicilan", JSON.stringify(status));
        updateTotal();
    };

});

function updateTotal() {
    document.getElementById("bayar").textContent =
        sudah.toLocaleString("id-ID");

    document.getElementById("sisa").textContent =
        (total - sudah).toLocaleString("id-ID");
}

updateTotal();
</script>
