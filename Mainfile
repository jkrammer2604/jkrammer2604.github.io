<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Zahlenverwaltung mit Supabase</title>
    <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2/dist/supabase.min.js"></script>

    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 40px;
            background-color: #f4f7fb;
        }
        input, button {
            padding: 8px;
            font-size: 16px;
            margin: 5px;
        }
        table {
            margin-top: 20px;
            border-collapse: collapse;
            width: 320px;
        }
        th, td {
            border: 1px solid #ccc;
            padding: 8px;
            text-align: center;
        }
        th {
            background-color: #ddd;
        }
        button.delete {
            background-color: #ff4d4d;
            color: white;
            border: none;
            cursor: pointer;
        }
    </style>
</head>
<body>

<h1>Zahlenverwaltung</h1>

<input type="number" id="zahlInput" placeholder="Zahl eingeben">
<button onclick="speichereZahl()">Speichern</button>

<table>
    <thead>
        <tr>
            <th>ID</th>
            <th>Zahl</th>
            <th>Löschen</th>
        </tr>
    </thead>
    <tbody id="zahlenListe"></tbody>
</table>

<script>
    // 🔗 Supabase Verbindung (FERTIG EINGEBAUT)
    const supabaseUrl = 'https://gdvctazobzciulavdvbh.supabase.co';
    const supabaseKey = 'sb_publishable_CVKgQ6u9Y1w0XaFlJ2da7w_WeyPpLa1';
    const supabase = Supabase.createClient(supabaseUrl, supabaseKey);

    // ➕ Zahl speichern
    async function speichereZahl() {
        const input = document.getElementById('zahlInput');
        const zahl = parseInt(input.value);

        if (isNaN(zahl)) {
            alert('Bitte eine gültige Zahl eingeben!');
            return;
        }

        await supabase
            .from('zahlencodes')
            .insert([{ zahl }]);

        input.value = '';
        ladeZahlen();
    }

    // 📥 Zahlen lesen
    async function ladeZahlen() {
        const { data, error } = await supabase
            .from('zahlencodes')
            .select('*')
            .order('id', { ascending: true });

        if (error) {
            alert(error.message);
            return;
        }

        const tbody = document.getElementById('zahlenListe');
        tbody.innerHTML = '';

        data.forEach(row => {
            const tr = document.createElement('tr');
            tr.innerHTML = `
                <td>${row.id}</td>
                <td>${row.zahl}</td>
                <td>
                    <button class="delete" onclick="loescheZahl(${row.id})">❌</button>
                </td>
            `;
            tbody.appendChild(tr);
        });
    }

    // ❌ Zahl löschen
    async function loescheZahl(id) {
        if (!confirm('Zahl wirklich löschen?')) return;

        await supabase
            .from('zahlencodes')
            .delete()
            .eq('id', id);

        ladeZahlen();
    }

    // 🔄 Beim Start laden
    ladeZahlen();
</script>

</body>
</html>
