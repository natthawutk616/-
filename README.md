"use client";

import {
  BarChart3,
  Users,
  Trophy,
  Lightbulb,
  Target,
  TrendingUp
} from "lucide-react";

import {
  ResponsiveContainer,
  PieChart,
  Pie,
  Cell,
  Tooltip,
  BarChart,
  Bar,
  XAxis,
  YAxis,
  CartesianGrid
} from "recharts";

import { motion } from "framer-motion";

const topicData = [
  { name: "Quality", value: 90 },
  { name: "Efficiency", value: 75 },
  { name: "Safety", value: 120 },
  { name: "Cost", value: 45 },
  { name: "Expense", value: 30 },
  { name: "Other", value: 15 },
];

const departmentData = [
  { name: "Emulsion", percent: 88 },
  { name: "Enamel", percent: 76 },
  { name: "QA", percent: 100 },
  { name: "SHE", percent: 95 },
  { name: "Tinting", percent: 82 },
];

const colors = [
  "#0EA5E9",
  "#22C55E",
  "#F59E0B",
  "#EF4444",
  "#8B5CF6",
  "#14B8A6",
];

const topSuggestions = [
  {
    rank: 1,
    name: "Natthawut",
    dept: "SHE",
    total: 38,
  },
  {
    rank: 2,
    name: "Somchai",
    dept: "QA",
    total: 34,
  },
  {
    rank: 3,
    name: "Wanida",
    dept: "Enamel",
    total: 28,
  },
];

export default function DashboardPage() {
  return (
    <div className="min-h-screen bg-slate-100 p-6">

      <div className="mb-8">
        <h1 className="text-4xl font-bold text-slate-800">
          Suggestion Dashboard
        </h1>

        <p className="text-slate-600 mt-2">
          Suggestion Management Portal
        </p>
      </div>

      {/* KPI Section */}

      <div className="grid lg:grid-cols-4 gap-5">

        <KPI
          title="Total Suggestions"
          value="423"
          icon={<Lightbulb />}
          color="bg-blue-500"
        />

        <KPI
          title="Participants"
          value="126"
          icon={<Users />}
          color="bg-green-500"
        />

        <KPI
          title="Goal Achievement"
          value="84.6%"
          icon={<Target />}
          color="bg-orange-500"
        />

        <KPI
          title="Best Department"
          value="SHE"
          icon={<Trophy />}
          color="bg-purple-600"
        />
      </div>

      {/* Goal Progress */}

      <div className="grid lg:grid-cols-3 gap-6 mt-8">

        <motion.div
          whileHover={{ scale: 1.02 }}
          className="bg-white rounded-3xl shadow-lg p-6"
        >
          <h2 className="font-bold text-xl mb-6">
            Annual Goal Progress
          </h2>

          <div className="flex justify-center">
            <div className="relative w-48 h-48">

              <div className="absolute inset-0 rounded-full border-[16px] border-gray-200"></div>

              <div
                className="absolute inset-0 rounded-full border-[16px] border-green-500"
                style={{
                  clipPath: "inset(0 0 25% 0)"
                }}
              />

              <div className="absolute inset-0 flex flex-col items-center justify-center">
                <div className="text-5xl font-bold text-green-600">
                  84%
                </div>

                <div className="text-sm text-gray-500">
                  423 / 500
                </div>
              </div>

            </div>
          </div>
        </motion.div>

        {/* Suggested Topics */}

        <div className="col-span-2 bg-white rounded-3xl shadow-lg p-6">
          <h2 className="text-xl font-bold mb-4">
            Suggested Topics
          </h2>

          <ResponsiveContainer width="100%" height={320}>
            <PieChart>

              <Pie
                data={topicData}
                cx="50%"
                cy="50%"
                outerRadius={120}
                dataKey="value"
                label
              >
                {topicData.map((entry, index) => (
                  <Cell
                    key={index}
                    fill={colors[index]}
                  />
                ))}
              </Pie>

              <Tooltip />
            </PieChart>
          </ResponsiveContainer>
        </div>
      </div>

      {/* Participation */}

      <div className="grid lg:grid-cols-2 gap-6 mt-8">

        <div className="bg-white rounded-3xl shadow-lg p-6">

          <div className="flex items-center gap-2 mb-4">
            <BarChart3 />
            <h2 className="font-bold text-xl">
              Participation by Department
            </h2>
          </div>

          <ResponsiveContainer width="100%" height={350}>

            <BarChart data={departmentData}>

              <CartesianGrid strokeDasharray="3 3" />

              <XAxis dataKey="name" />

              <YAxis />

              <Tooltip />

              <Bar
                dataKey="percent"
                fill="#0F4C81"
                radius={[10, 10, 0, 0]}
              />

            </BarChart>

          </ResponsiveContainer>

        </div>

        {/* Top Contributors */}

        <div className="bg-white rounded-3xl shadow-lg p-6">

          <div className="flex items-center gap-2 mb-4">
            <TrendingUp />
            <h2 className="font-bold text-xl">
              Top Contributors
            </h2>
          </div>

          <div className="space-y-4">

            {topSuggestions.map((person) => (

              <motion.div
                key={person.rank}
                whileHover={{ scale: 1.03 }}
                className="border rounded-2xl p-4 flex justify-between items-center"
              >
                <div>

                  <div className="text-lg font-semibold">
                    #{person.rank} {person.name}
                  </div>

                  <div className="text-gray-500">
                    {person.dept}
                  </div>

                </div>

                <div className="text-right">

                  <div className="text-2xl font-bold text-blue-600">
                    {person.total}
                  </div>

                  <div className="text-sm text-gray-500">
                    Suggestions
                  </div>

                </div>

              </motion.div>

            ))}

          </div>

        </div>

      </div>

      {/* Best Suggestion */}

      <div className="bg-white rounded-3xl shadow-lg p-6 mt-8">

        <h2 className="font-bold text-2xl mb-6">
          Best Suggestion Award
        </h2>

        <div className="overflow-x-auto">

          <table className="w-full">

            <thead>

              <tr className="bg-slate-100">

                <th className="p-4 text-left">Employee</th>
                <th className="p-4">Self</th>
                <th className="p-4">Operation</th>
                <th className="p-4">Sustainability</th>
                <th className="p-4">Alignment</th>
                <th className="p-4">Total</th>

              </tr>

            </thead>

            <tbody>

              <tr className="border-b">

                <td className="p-4">
                  Natthawut Krungkraijak
                </td>

                <td className="text-center">
                  30
                </td>

                <td className="text-center">
                  28
                </td>

                <td className="text-center">
                  20
                </td>

                <td className="text-center">
                  18
                </td>

                <td className="text-center font-bold text-green-600">
                  96
                </td>

              </tr>

            </tbody>

          </table>

        </div>

      </div>

    </div>
  );
}

function KPI({
  title,
  value,
  icon,
  color,
}: {
  title: string;
  value: string;
  icon: React.ReactNode;
  color: string;
}) {
  return (
    <motion.div
      whileHover={{ scale: 1.04 }}
      className="bg-white rounded-3xl shadow-lg p-5"
    >
      <div className="flex items-center justify-between">

        <div>

          <div className="text-slate-500 text-sm">
            {title}
          </div>

          <div className="text-3xl font-bold mt-2">
            {value}
          </div>

        </div>

        <div
          className={`w-14 h-14 rounded-2xl ${color} text-white flex items-center justify-center`}
        >
          {icon}
        </div>

      </div>
    </motion.div>
  );
}
