import { useState } from 'react'; import { Card, CardContent } from "@/components/ui/card"; import { Button } from "@/components/ui/button"; import { Calendar } from "lucide-react";

const fakeAppointments = { Monday: [], Tuesday: [ { time: "4:30 PM", name: "John Doe", address: "123 Maple St", status: "Confirmed" }, { time: "5:30 PM", name: "Sarah Kim", address: "456 Pine Ave", status: "Confirmed" }, ], Wednesday: [ { time: "6:30 PM", name: "Nina Rivera", address: "789 Cedar Blvd", status: "Confirmed" }, ], Saturday: [ { time: "8:00 AM", name: "Tom Newman", address: "12 Elm St", status: "Confirmed" }, { time: "10:00 AM", name: "Emily Chan", address: "34 Oak Ave", status: "Confirmed" }, { time: "12:00 PM", name: "Leo Turner", address: "56 Spruce Rd", status: "Confirmed" }, ] };

export default function DemoScheduler() { const [appointments, setAppointments] = useState(fakeAppointments); const [status, setStatus] = useState("No new emails yet.");

const handleCheckEmails = () => { setStatus("3 new appointment requests found. 2 scheduled, 1 waiting on reply."); };

return ( <div className="p-4 space-y-6"> <h1 className="text-2xl font-bold">Lawn Aeration Scheduler</h1> <div className="flex items-center gap-4"> <Button onClick={handleCheckEmails}>Check for New Appointment Requests</Button> <p className="text-green-600 font-semibold">{status}</p> </div>

<div className="grid grid-cols-2 md:grid-cols-4 gap-4">
    {Object.keys(appointments).map((day) => (
      <Card key={day}>
        <CardContent className="p-4">
          <h2 className="font-semibold text-lg mb-2 flex items-center gap-2">
            <Calendar className="w-4 h-4" /> {day}
          </h2>
          {appointments[day].length === 0 ? (
            <p className="text-gray-400">No appointments</p>
          ) : (
            appointments[day].map((appt, index) => (
              <div key={index} className="mb-2 p-2 bg-green-50 rounded-lg">
                <p className="text-sm font-medium">{appt.time} - {appt.name}</p>
                <p className="text-xs text-gray-600">{appt.address}</p>
                <p className="text-xs text-green-600">{appt.status}</p>
              </div>
            ))
          )}
        </CardContent>
      </Card>
    ))}
  </div>
</div>

); }

