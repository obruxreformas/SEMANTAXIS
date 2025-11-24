import type { Metadata } from "next";
import { Inter, Playfair_Display } from "next/font/google";
import "./globals.css";

const inter = Inter({ subsets: ["latin"], variable: '--font-inter' });
const playfair = Playfair_Display({ subsets: ["latin"], variable: '--font-playfair' });

export const metadata: Metadata = {
  title: "SEMANTAXIS | Revista Científica",
  description: "Plataforma de investigación y publicación científica con IA.",
};

export default function RootLayout({
  children,
}: Readonly<{
  children: React.ReactNode;
}>) {
  return (
    <html lang="es">
      <body className={`${inter.variable} ${playfair.variable} font-sans bg-slate-50 text-slate-900`}>
        <nav className="w-full bg-white border-b border-gray-200 sticky top-0 z-50">
          <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex justify-between items-center">
            <span className="font-serif text-2xl font-bold tracking-tighter">SEMANTAXIS</span>
            <div className="flex gap-4 text-sm font-medium">
              <a href="/" className="hover:text-blue-600">Inicio</a>
              <a href="/archivo" className="hover:text-blue-600">Archivo</a>
              <a href="/dashboard" className="bg-black text-white px-4 py-2 rounded-full hover:bg-gray-800 transition">
                Acceso Autores/Evaluadores
              </a>
            </div>
          </div>
        </nav>
        {children}
        <footer className="bg-gray-900 text-white py-12 mt-20">
          <div className="max-w-7xl mx-auto px-4 text-center">
            <p>© 2024 SEMANTAXIS. Ciencia abierta y tecnología.</p>
          </div>
        </footer>
      </body>
    </html>
  );
}
2. Página Principal (El Diagnóstico/Lectura) (app/page.tsx)
import { FileText, BookOpen, Users, Download } from 'lucide-react';

// Datos simulados (esto vendría de Supabase)
const currentIssue = {
  vol: "Vol. 4",
  num: "No. 2 (2024)",
  title: "Inteligencia Artificial en la Educación Superior",
  coverImage: "/api/placeholder/400/600", // Reemplazar con url real
  editorial: "Hacia una nueva era del conocimiento automatizado",
  articles: [
    { id: 1, title: "Impacto de los LLMs en la pedagogía", author: "Dra. María Pérez", keywords: ["IA", "Educación", "LLM"], pdf: "#" },
    { id: 2, title: "Ética algorítmica en la investigación", author: "Dr. Juan Roa", keywords: ["Ética", "Algoritmos"], pdf: "#" },
    { id: 3, title: "Sistemas de evaluación automatizada", author: "Mg. Luisa Lane", keywords: ["Evaluación", "Sistemas"], pdf: "#" },
  ]
};

export default function Home() {
  return (
    <main className="min-h-screen">
      {/* Hero Section - Portada */}
      <section className="relative bg-slate-900 text-white py-20">
        <div className="max-w-7xl mx-auto px-4 grid md:grid-cols-2 gap-12 items-center">
          <div className="space-y-6">
            <span className="inline-block bg-blue-600 text-xs px-3 py-1 rounded-full uppercase tracking-wide font-bold">
              Número Actual
            </span>
            <h1 className="font-serif text-5xl md:text-6xl leading-tight">
              {currentIssue.title}
            </h1>
            <p className="text-gray-300 text-lg">{currentIssue.vol} - {currentIssue.num}</p>
            <div className="flex gap-4 pt-4">
              <button className="flex items-center gap-2 bg-white text-black px-6 py-3 rounded-lg font-bold hover:bg-gray-100 transition">
                <BookOpen size={20} /> Leer Editorial
              </button>
              <button className="flex items-center gap-2 border border-white px-6 py-3 rounded-lg font-bold hover:bg-white/10 transition">
                <Users size={20} /> Ver Comité
              </button>
            </div>
          </div>
          {/* Simulación de Portada */}
          <div className="flex justify-center">
            <div className="w-80 h-[480px] bg-gray-700 shadow-2xl rounded-sm flex items-center justify-center relative border-l-4 border-white/20">
              <span className="text-white/50 font-serif text-2xl">Portada.pdf</span>
            </div>
          </div>
        </div>
      </section>

      {/* Índice y Artículos */}
      <section className="max-w-5xl mx-auto px-4 py-20">
        <h2 className="font-serif text-3xl font-bold mb-12 text-center border-b pb-4">Índice de Contenidos</h2>
        
        <div className="grid gap-8">
          {/* Páginas Legales */}
          <div className="bg-white p-6 rounded-xl shadow-sm border border-gray-100 flex justify-between items-center hover:shadow-md transition">
             <div className="flex items-center gap-4">
                <div className="p-3 bg-gray-100 rounded-lg"><FileText size={24} className="text-gray-600"/></div>
                <div>
                  <h3 className="font-bold text-lg">Páginas Legales e Institucionales</h3>
                  <p className="text-sm text-gray-500">ISSN: 2024-000X</p>
                </div>
             </div>
             <button className="text-blue-600 font-medium hover:underline">Ver PDF</button>
          </div>

          {/* Lista de Artículos */}
          {currentIssue.articles.map((art) => (
            <article key={art.id} className="group bg-white p-8 rounded-xl shadow-sm border border-gray-100 hover:border-blue-500 transition relative overflow-hidden">
              <div className="flex flex-col md:flex-row justify-between gap-6">
                <div className="space-y-3">
                  <h3 className="font-serif text-2xl font-bold text-gray-900 group-hover:text-blue-700 transition">
                    {art.title}
                  </h3>
                  <p className="text-gray-600 font-medium">{art.author}</p>
                  {/* Metadata IA */}
                  <div className="flex gap-2 flex-wrap">
                    {art.keywords.map(k => (
                      <span key={k} className="bg-blue-50 text-blue-700 text-xs px-2 py-1 rounded border border-blue-100">
                        #{k}
                      </span>
                    ))}
                  </div>
                </div>
                <div className="flex flex-col justify-center gap-3 min-w-[140px]">
                   <a href={art.pdf} className="flex items-center justify-center gap-2 bg-slate-900 text-white px-4 py-2 rounded-lg hover:bg-slate-800 transition text-sm">
                     <Download size={16} /> Descargar PDF
                   </a>
                   <button className="text-xs text-gray-500 text-center hover:text-black">Ver Referencias</button>
                </div>
              </div>
            </article>
          ))}
        </div>
      </section>
    </main>
  );
}
3. El Dashboard (La Magia - Gestión) (app/dashboard/page.tsx)
"use client";
import { useState } from 'react';
import { Upload, CheckCircle, FileSearch, Award } from 'lucide-react';

export default function Dashboard() {
  // En una app real, esto se determina por el rol del usuario logueado
  const [role, setRole] = useState<'author' | 'reviewer'>('author');

  return (
    <div className="min-h-screen bg-slate-50 p-8">
      <div className="max-w-6xl mx-auto">
        
        {/* Header del Dashboard */}
        <header className="flex justify-between items-center mb-10">
          <div>
            <h1 className="font-serif text-3xl font-bold">Panel de Control</h1>
            <p className="text-gray-500">Bienvenido a SEMANTAXIS</p>
          </div>
          <div className="bg-white p-1 rounded-lg border shadow-sm">
            <button 
              onClick={() => setRole('author')}
              className={`px-4 py-2 rounded-md text-sm font-medium transition ${role === 'author' ? 'bg-blue-600 text-white' : 'text-gray-600 hover:bg-gray-50'}`}
            >
              Vista Autor
            </button>
            <button 
              onClick={() => setRole('reviewer')}
              className={`px-4 py-2 rounded-md text-sm font-medium transition ${role === 'reviewer' ? 'bg-purple-600 text-white' : 'text-gray-600 hover:bg-gray-50'}`}
            >
              Vista Evaluador
            </button>
          </div>
        </header>

        {/* VISTA DEL AUTOR */}
        {role === 'author' && (
          <div className="grid md:grid-cols-3 gap-6">
            {/* Tarjeta de Envío */}
            <div className="md:col-span-2 bg-white p-8 rounded-xl shadow-sm border border-gray-200">
              <h2 className="font-bold text-xl mb-6 flex items-center gap-2">
                <Upload className="text-blue-600"/> Enviar Nuevo Artículo
              </h2>
              <form className="space-y-4">
                <div>
                  <label className="block text-sm font-medium mb-1">Título del Artículo</label>
                  <input type="text" className="w-full border rounded-lg p-2" placeholder="Ingrese el título..." />
                </div>
                <div>
                  <label className="block text-sm font-medium mb-1">Resumen (Abstract)</label>
                  <textarea className="w-full border rounded-lg p-2 h-32" placeholder="Pegue el resumen aquí. La IA generará los keywords automáticamente..."></textarea>
                  <p className="text-xs text-blue-600 mt-1 flex items-center gap-1">
                    ✨ La IA analizará este texto para posicionamiento SEO.
                  </p>
                </div>
                <div className="border-2 border-dashed border-gray-300 rounded-lg p-8 text-center hover:bg-gray-50 cursor-pointer transition">
                  <p className="text-gray-500">Arrastra tu archivo Word o LaTeX aquí</p>
                </div>
                <button className="w-full bg-blue-600 text-white py-3 rounded-lg font-bold hover:bg-blue-700">
                  Enviar a Revisión
                </button>
              </form>
            </div>

            {/* Estado */}
            <div className="space-y-6">
              <div className="bg-white p-6 rounded-xl shadow-sm border-l-4 border-yellow-400">
                <h3 className="font-bold text-gray-900">En Revisión</h3>
                <p className="text-sm text-gray-500 mt-1">"Metodologías Ágiles..."</p>
                <div className="mt-4 text-xs bg-yellow-50 text-yellow-700 px-2 py-1 rounded inline-block">
                  Fase: Evaluación por Pares
                </div>
              </div>
              <div className="bg-white p-6 rounded-xl shadow-sm border-l-4 border-green-500">
                <h3 className="font-bold text-gray-900">Publicado</h3>
                <p className="text-sm text-gray-500 mt-1">"Historia del Arte..."</p>
                <button className="mt-4 text-xs text-blue-600 font-bold hover:underline">Ver Métricas</button>
              </div>
            </div>
          </div>
        )}

        {/* VISTA DEL EVALUADOR */}
        {role === 'reviewer' && (
          <div className="grid gap-6">
             <div className="bg-purple-50 border border-purple-100 p-6 rounded-xl flex items-center gap-4">
                <Award className="text-purple-600" size={32} />
                <div>
                  <h2 className="font-bold text-purple-900">Nivel de Revisor: Experto</h2>
                  <p className="text-purple-700 text-sm">Has completado 12 revisiones este año. ¡Gracias!</p>
                </div>
             </div>

             <div className="bg-white rounded-xl shadow-sm border overflow-hidden">
               <div className="p-6 border-b">
                 <h3 className="font-bold text-lg">Artículos Asignados para Revisión</h3>
               </div>
               <div className="divide-y">
                 {[1, 2].map((item) => (
                   <div key={item} className="p-6 flex justify-between items-center hover:bg-gray-50">
                     <div>
                       <h4 className="font-medium text-gray-900">Análisis de Big Data en Ciencias Sociales</h4>
                       <p className="text-sm text-gray-500">Fecha límite: 30 Nov 2024</p>
                     </div>
                     <button className="flex items-center gap-2 bg-slate-900 text-white px-4 py-2 rounded-lg text-sm hover:bg-slate-800">
                       <FileSearch size={16}/> Evaluar Ahora
                     </button>
                   </div>
                 ))}
               </div>
             </div>
          </div>
        )}

      </div>
    </div>
  );
}
