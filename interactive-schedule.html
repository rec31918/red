import React, { useState, useEffect } from 'react';
import { Calendar, DollarSign, Users, AlertCircle, Download, Save, Loader2 } from 'lucide-react';

const CaregiverScheduler = () => {
  const caregivers = [
    { name: 'Marie', rate: 27, preference: 'Nights', commitment: '3-4 nights/week', color: '#8B5CF6', prn: false },
    { name: 'Dannie', rate: 32, preference: 'Days', commitment: '4-5 days/week', color: '#3B82F6', prn: false },
    { name: 'Hana', rate: 27, preference: 'Friday Nights ONLY', commitment: '1 night/week (Fri only)', color: '#EC4899', prn: false },
    { name: 'Sweta', rate: 30, preference: 'Thu & Sat Nights ONLY', commitment: '2 nights/week (Thu & Sat only)', color: '#10B981', prn: false },
    { name: 'Netsie', rate: 27, preference: 'Thursday Days ONLY', commitment: '1 day/week (Thu only)', color: '#F59E0B', prn: false },
    { name: 'Nate (Day)', rate: 40, preference: 'PRN Days', commitment: 'As needed ($40/hr)', color: '#6366F1', prn: true },
    { name: 'Nate (Night)', rate: 30, preference: 'PRN Nights (Preferred)', commitment: 'As needed ($30/hr)', color: '#6366F1', prn: true },
    { name: 'Christine', rate: 30, preference: 'Weekdays Only', commitment: 'Fill-in ($30/hr)', color: '#EF4444', prn: false }
  ];

  const days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
  const shifts = ['Day (8am-8pm)', 'Night (8pm-8am)'];

  const [schedule, setSchedule] = useState({});
  const [selectedWeek, setSelectedWeek] = useState('');
  const [loading, setLoading] = useState(true);
  const [saving, setSaving] = useState(false);

  // Generate week identifier (e.g., "2025-W43") - always starts on Sunday
  const getWeekIdentifier = (date = new Date()) => {
    const d = new Date(date);
    d.setHours(0, 0, 0, 0);
    
    // Get the Sunday of the current week
    const dayOfWeek = d.getDay();
    const sunday = new Date(d);
    sunday.setDate(d.getDate() - dayOfWeek);
    
    // Calculate week number based on the year's first Sunday
    const yearStart = new Date(sunday.getFullYear(), 0, 1);
    const firstSunday = new Date(yearStart);
    const firstSundayDay = firstSunday.getDay();
    if (firstSundayDay !== 0) {
      firstSunday.setDate(yearStart.getDate() + (7 - firstSundayDay));
    }
    
    const weekNo = Math.ceil((sunday - firstSunday) / (7 * 24 * 60 * 60 * 1000)) + 1;
    return `${sunday.getFullYear()}-W${weekNo}`;
  };

  const getWeekDisplay = (weekId) => {
    if (!weekId) return '';
    const [year, week] = weekId.split('-W');
    
    // Calculate the Sunday for this week
    const yearStart = new Date(year, 0, 1);
    const firstSunday = new Date(yearStart);
    const firstSundayDay = firstSunday.getDay();
    if (firstSundayDay !== 0) {
      firstSunday.setDate(yearStart.getDate() + (7 - firstSundayDay));
    }
    
    const sunday = new Date(firstSunday);
    sunday.setDate(firstSunday.getDate() + (week - 1) * 7);
    
    const saturday = new Date(sunday);
    saturday.setDate(sunday.getDate() + 6);
    
    return `${sunday.toLocaleDateString('en-US', { month: 'short', day: 'numeric' })} - ${saturday.toLocaleDateString('en-US', { month: 'short', day: 'numeric', year: 'numeric' })}`;
  };

  useEffect(() => {
    const currentWeek = getWeekIdentifier();
    setSelectedWeek(currentWeek);
    loadSchedule(currentWeek);
  }, []);

  const loadSchedule = async (weekId) => {
    setLoading(true);
    try {
      const result = await window.storage.get(`schedule-${weekId}`, false);
      if (result && result.value) {
        setSchedule(JSON.parse(result.value));
      } else {
        setSchedule({});
      }
    } catch (error) {
      console.log('No existing schedule found, starting fresh');
      setSchedule({});
    }
    setLoading(false);
  };

  const saveSchedule = async () => {
    setSaving(true);
    try {
      await window.storage.set(`schedule-${selectedWeek}`, JSON.stringify(schedule), false);
      alert('Schedule saved successfully!');
    } catch (error) {
      console.error('Error saving schedule:', error);
      alert('Error saving schedule. Please try again.');
    }
    setSaving(false);
  };

  const handleShiftChange = (day, shift, caregiver) => {
    setSchedule(prev => ({
      ...prev,
      [`${day}-${shift}`]: caregiver
    }));
  };

  const calculateWeeklyHours = () => {
    const hours = {};
    caregivers.forEach(cg => {
      hours[cg.name] = 0;
    });

    Object.entries(schedule).forEach(([key, caregiver]) => {
      if (caregiver && hours[caregiver] !== undefined) {
        hours[caregiver] += 12;
      }
    });

    return hours;
  };

  const calculateWeeklyPay = () => {
    const hours = calculateWeeklyHours();
    const pay = {};
    
    caregivers.forEach(cg => {
      pay[cg.name] = {
        hours: hours[cg.name],
        rate: cg.rate,
        total: hours[cg.name] * cg.rate
      };
    });

    return pay;
  };

  const getCoverageGaps = () => {
    const gaps = [];
    days.forEach(day => {
      shifts.forEach(shift => {
        const key = `${day}-${shift}`;
        if (!schedule[key]) {
          gaps.push(`${day} - ${shift}`);
        }
      });
    });
    return gaps;
  };

  const exportToCSV = () => {
    const pay = calculateWeeklyPay();
    let csv = 'Caregiver,Hours,Rate,Total Pay\n';
    
    Object.entries(pay).forEach(([name, data]) => {
      if (data.hours > 0) {
        csv += `${name},${data.hours},$${data.rate},$${data.total.toFixed(2)}\n`;
      }
    });

    const blob = new Blob([csv], { type: 'text/csv' });
    const url = window.URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = `caregiver-pay-${selectedWeek}.csv`;
    a.click();
  };

  const changeWeek = (direction) => {
    const [year, week] = selectedWeek.split('-W');
    let newWeek = parseInt(week) + direction;
    let newYear = parseInt(year);
    
    if (newWeek > 52) {
      newWeek = 1;
      newYear++;
    } else if (newWeek < 1) {
      newWeek = 52;
      newYear--;
    }
    
    const newWeekId = `${newYear}-W${newWeek}`;
    setSelectedWeek(newWeekId);
    loadSchedule(newWeekId);
  };

  const weeklyHours = calculateWeeklyHours();
  const weeklyPay = calculateWeeklyPay();
  const gaps = getCoverageGaps();
  const totalWeeklyPay = Object.values(weeklyPay).reduce((sum, p) => sum + p.total, 0);

  if (loading) {
    return (
      <div className="flex items-center justify-center min-h-screen bg-gray-50">
        <Loader2 className="w-8 h-8 animate-spin text-blue-600" />
      </div>
    );
  }

  return (
    <div className="min-h-screen bg-gray-50 p-4 md:p-8">
      <div className="max-w-7xl mx-auto">
        {/* Header */}
        <div className="bg-white rounded-lg shadow-sm p-6 mb-6">
          <div className="flex items-center justify-between mb-4">
            <div>
              <h1 className="text-3xl font-bold text-gray-900 flex items-center gap-2">
                <Calendar className="w-8 h-8 text-blue-600" />
                Caregiver Schedule Manager
              </h1>
              <p className="text-gray-600 mt-1">24/7 Care Coordination & Payment Tracking</p>
            </div>
            <button
              onClick={saveSchedule}
              disabled={saving}
              className="flex items-center gap-2 bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 disabled:bg-gray-400"
            >
              {saving ? <Loader2 className="w-4 h-4 animate-spin" /> : <Save className="w-4 h-4" />}
              {saving ? 'Saving...' : 'Save Schedule'}
            </button>
          </div>

          {/* Week Navigation */}
          <div className="flex items-center justify-between bg-gray-50 p-4 rounded-lg">
            <button
              onClick={() => changeWeek(-1)}
              className="px-4 py-2 bg-white border border-gray-300 rounded-lg hover:bg-gray-50"
            >
              ← Previous Week
            </button>
            <div className="text-center">
              <div className="text-sm text-gray-600">Week of</div>
              <div className="text-lg font-semibold text-gray-900">{getWeekDisplay(selectedWeek)}</div>
            </div>
            <button
              onClick={() => changeWeek(1)}
              className="px-4 py-2 bg-white border border-gray-300 rounded-lg hover:bg-gray-50"
            >
              Next Week →
            </button>
          </div>

          {/* Coverage Gaps Alert */}
          {gaps.length > 0 && (
            <div className="mt-4 bg-red-50 border border-red-200 rounded-lg p-4">
              <div className="flex items-start gap-2">
                <AlertCircle className="w-5 h-5 text-red-600 flex-shrink-0 mt-0.5" />
                <div>
                  <h3 className="font-semibold text-red-900">Coverage Gaps Detected</h3>
                  <p className="text-sm text-red-700 mt-1">{gaps.join(', ')}</p>
                </div>
              </div>
            </div>
          )}
        </div>

        {/* Schedule Grid */}
        <div className="bg-white rounded-lg shadow-sm p-6 mb-6">
          <h2 className="text-xl font-bold text-gray-900 mb-4">Weekly Schedule</h2>
          <div className="overflow-x-auto">
            <table className="w-full border-collapse">
              <thead>
                <tr>
                  <th className="border border-gray-300 bg-gray-50 p-3 text-left font-semibold">Day</th>
                  <th className="border border-gray-300 bg-blue-50 p-3 text-left font-semibold">Day Shift (8am-8pm)</th>
                  <th className="border border-gray-300 bg-indigo-50 p-3 text-left font-semibold">Night Shift (8pm-8am)</th>
                </tr>
              </thead>
              <tbody>
                {days.map(day => (
                  <tr key={day}>
                    <td className="border border-gray-300 p-3 font-medium bg-gray-50">{day}</td>
                    {shifts.map(shift => {
                      const key = `${day}-${shift}`;
                      const assigned = schedule[key];
                      const caregiver = caregivers.find(c => c.name === assigned);
                      
                      return (
                        <td key={shift} className="border border-gray-300 p-2">
                          <select
                            value={schedule[key] || ''}
                            onChange={(e) => handleShiftChange(day, shift, e.target.value)}
                            className="w-full p-2 border border-gray-300 rounded focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
                            style={{
                              backgroundColor: caregiver ? `${caregiver.color}15` : 'white',
                              borderColor: caregiver ? caregiver.color : '#d1d5db'
                            }}
                          >
                            <option value="">-- Unassigned --</option>
                            <option value="Marie">Marie</option>
                            <option value="Dannie">Dannie</option>
                            <option value="Hana">Hana</option>
                            <option value="Sweta">Sweta</option>
                            <option value="Netsie">Netsie</option>
                            <option value="Nate (Day)">Nate (Day)</option>
                            <option value="Nate (Night)">Nate (Night)</option>
                            <option value="Christine">Christine</option>
                          </select>
                          {caregiver && (
                            <div className="text-xs text-gray-600 mt-1">
                              Prefers: {caregiver.preference}
                            </div>
                          )}
                        </td>
                      );
                    })}
                  </tr>
                ))}
              </tbody>
            </table>
          </div>
        </div>

        {/* Caregiver Reference */}
        <div className="bg-white rounded-lg shadow-sm p-6 mb-6">
          <h2 className="text-xl font-bold text-gray-900 mb-4 flex items-center gap-2">
            <Users className="w-5 h-5" />
            Caregiver Reference
          </h2>
          <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
            {caregivers.map(cg => (
              <div
                key={cg.name}
                className="border-l-4 p-4 bg-gray-50 rounded"
                style={{ borderColor: cg.color }}
              >
                <div className="font-semibold text-gray-900">{cg.name}</div>
                <div className="text-sm text-gray-600 mt-1">Prefers: {cg.preference}</div>
                <div className="text-sm text-gray-600">Commitment: {cg.commitment}</div>
                {cg.prn && (
                  <div className="text-xs text-red-600 mt-1 font-semibold">PRN (As Needed)</div>
                )}
              </div>
            ))}
          </div>
        </div>

        {/* Payment Summary */}
        <div className="bg-white rounded-lg shadow-sm p-6">
          <div className="flex items-center justify-between mb-4">
            <h2 className="text-xl font-bold text-gray-900 flex items-center gap-2">
              <DollarSign className="w-5 h-5" />
              Weekly Payment Summary (Private - Only Visible to You)
            </h2>
            <button
              onClick={exportToCSV}
              className="flex items-center gap-2 bg-green-600 text-white px-4 py-2 rounded-lg hover:bg-green-700"
            >
              <Download className="w-4 h-4" />
              Export to CSV
            </button>
          </div>

          <div className="overflow-x-auto">
            <table className="w-full">
              <thead>
                <tr className="border-b-2 border-gray-300">
                  <th className="text-left p-3 font-semibold">Caregiver</th>
                  <th className="text-right p-3 font-semibold">Hours</th>
                  <th className="text-right p-3 font-semibold">Rate</th>
                  <th className="text-right p-3 font-semibold">Total Pay</th>
                </tr>
              </thead>
              <tbody>
                {Object.entries(weeklyPay)
                  .filter(([_, data]) => data.hours > 0)
                  .map(([name, data]) => {
                    const cg = caregivers.find(c => c.name === name);
                    return (
                      <tr key={name} className="border-b border-gray-200">
                        <td className="p-3">
                          <div className="flex items-center gap-2">
                            <div
                              className="w-3 h-3 rounded-full"
                              style={{ backgroundColor: cg.color }}
                            />
                            {name}
                          </div>
                        </td>
                        <td className="text-right p-3">{data.hours} hrs</td>
                        <td className="text-right p-3">${data.rate.toFixed(2)}</td>
                        <td className="text-right p-3 font-semibold">${data.total.toFixed(2)}</td>
                      </tr>
                    );
                  })}
                <tr className="bg-gray-50 font-bold">
                  <td className="p-3">TOTAL</td>
                  <td className="text-right p-3">
                    {Object.values(weeklyPay).reduce((sum, p) => sum + p.hours, 0)} hrs
                  </td>
                  <td className="text-right p-3">-</td>
                  <td className="text-right p-3">${totalWeeklyPay.toFixed(2)}</td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  );
};

export default CaregiverScheduler;