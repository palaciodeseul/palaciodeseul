- 👋 Hi, I’m @palaciodeseul
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
palaciodeseul/palaciodeseul is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import React, { useState } from "react";
import { BrowserRouter as Router, Route, Routes, Link } from "react-router-dom";
import { Card, CardContent } from "@/components/ui/card";

const Home = () => (
  <div className="text-center p-10">
    <h1 className="text-4xl font-bold">Bienvenido a Palacio de Seúl</h1>
    <p className="mt-4">Auténtica comida coreana en un ambiente acogedor.</p>
    <img
      src="https://source.unsplash.com/800x400/?korean-food"
      alt="Comida coreana"
      className="rounded-xl mt-4 mx-auto"
    />
  </div>
);

const Menu = () => (
  <div className="p-10">
    <h2 className="text-3xl font-bold mb-4">Nuestro Menú</h2>
    <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
      {["Kimchi", "Bibimbap", "Tteokbokki", "Bulgogi", "Jajangmyeon"].map((item, index) => (
        <Card key={index} className="p-4 shadow-lg">
          <CardContent>
            <h3 className="text-xl font-semibold">{item}</h3>
            <p>Delicioso platillo coreano.</p>
            <p className="text-lg font-bold mt-2">$12.99</p>
          </CardContent>
        </Card>
      ))}
    </div>
  </div>
);

const About = () => (
  <div className="p-10 text-center">
    <h2 className="text-3xl font-bold">Sobre Nosotros</h2>
    <p className="mt-4">En Palacio de Seúl, nos apasiona traer lo mejor de la gastronomía coreana a tu mesa.</p>
  </div>
);

const Contact = () => (
  <div className="p-10 text-center">
    <h2 className="text-3xl font-bold">Contáctanos</h2>
    <p className="mt-4">📍 Dirección: Calle Principal 123, Ciudad</p>
    <p>📞 Teléfono: +123 456 7890</p>
    <p>📧 Email: contacto@palaciodeseul.com</p>
  </div>
);

const Reservation = () => {
  const [name, setName] = useState("");
  const [date, setDate] = useState("");
  const [time, setTime] = useState("");
  const [guests, setGuests] = useState(1);
  const [message, setMessage] = useState("");

  const handleSubmit = async (e) => {
    e.preventDefault();
    const reservationData = { name, date, time, guests };

    try {
      const response = await fetch("https://your-backend-api.com/reservations", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(reservationData),
      });

      if (response.ok) {
        setMessage(`Reserva confirmada para ${name} el ${date} a las ${time} para ${guests} personas.`);
      } else {
        setMessage("Error al realizar la reserva. Inténtalo de nuevo.");
      }
    } catch (error) {
      setMessage("No se pudo conectar con el servidor. Inténtalo más tarde.");
    }
  };

  return (
    <div className="p-10 text-center">
      <h2 className="text-3xl font-bold">Reservar una Mesa</h2>
      <form onSubmit={handleSubmit} className="mt-4 space-y-4 max-w-md mx-auto">
        <input type="text" placeholder="Nombre" className="w-full p-2 border rounded" value={name} onChange={(e) => setName(e.target.value)} required />
        <input type="date" className="w-full p-2 border rounded" value={date} onChange={(e) => setDate(e.target.value)} required />
        <input type="time" className="w-full p-2 border rounded" value={time} onChange={(e) => setTime(e.target.value)} required />
        <input type="number" min="1" max="10" className="w-full p-2 border rounded" value={guests} onChange={(e) => setGuests(e.target.value)} required />
        <button type="submit" className="bg-gray-800 text-white px-4 py-2 rounded">Reservar</button>
      </form>
      {message && <p className="mt-4 text-green-600 font-bold">{message}</p>}
    </div>
  );
};

const Navbar = () => (
  <nav className="bg-gray-800 p-4 text-white flex justify-around">
    <Link to="/" className="hover:text-gray-300">Inicio</Link>
    <Link to="/menu" className="hover:text-gray-300">Menú</Link>
    <Link to="/about" className="hover:text-gray-300">Sobre Nosotros</Link>
    <Link to="/contact" className="hover:text-gray-300">Contacto</Link>
    <Link to="/reservation" className="hover:text-gray-300">Reservar</Link>
  </nav>
);

const App = () => {
  return (
    <Router>
      <Navbar />
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/menu" element={<Menu />} />
        <Route path="/about" element={<About />} />
        <Route path="/contact" element={<Contact />} />
        <Route path="/reservation" element={<Reservation />} />
      </Routes>
    </Router>
  );
};

export default App;
