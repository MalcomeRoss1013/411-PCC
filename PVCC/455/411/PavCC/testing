import React, { useState } from 'react';

function App() {
  const [forms, setForms] = useState([
    {
      data: [
        {
          included: 'y',
          quantity: 1,
          description: 'brick',
          type: 'material',
          cost: 850.0,
          'total(no markup)': 1190.0,
          total: 850.0,
          expense: 1190.0,
          revenue: '',
          Pricing: '',
          OurCost: '',
          JobProfit: '',
        },
        // Add more initial entries for the first form as needed
      ],
      columns: [
        'included',
        'quantity',
        'description',
        'type',
        'cost',
        'total(no markup)',
        'total',
        'expense',
        'revenue',
        'Pricing',
        'OurCost',
        'JobProfit',
      ],
      columnVisibility: {},
    },
  ]);

  const [currentFormIndex, setCurrentFormIndex] = useState(0);



  const handleQuantityChange = (formIndex, rowIndex, newQuantity) => {
    const form = forms[formIndex];
    const updatedData = [...form.data];
    updatedData[rowIndex].quantity = parseInt(newQuantity, 10) || 0;
    const updatedForms = [...forms];
    updatedForms[formIndex].data = updatedData;
    setForms(updatedForms);
  };

  const toggleColumnVisibility = (formIndex, columnName) => {
    setForms((prevForms) => {
      const updatedForms = [...prevForms];
      updatedForms[formIndex].columnVisibility[columnName] =
        !updatedForms[formIndex].columnVisibility[columnName];
      return updatedForms;
    });
  };

  const addNewEntry = (formIndex) => {
    const form = forms[formIndex];
    const newEntry = {};
    form.columns.forEach((column) => {
      newEntry[column] = column === 'quantity' ? 0 : '';
    });
    const updatedData = [...form.data, newEntry];
    const updatedForms = [...forms];
    updatedForms[formIndex].data = updatedData;
    setForms(updatedForms);
  };

  const addNewColumn = (formIndex) => {
    const form = forms[formIndex];
    const newColumnName = prompt('Enter the name for the new column:');
    if (newColumnName) {
      const updatedColumns = [...form.columns, newColumnName];
      const updatedForms = [...forms];
      updatedForms[formIndex].columns = updatedColumns;
      updatedForms[formIndex].columnVisibility[newColumnName] = true;
      setForms(updatedForms);
    }
  };

  const createNewForm = () => {
    setForms((prevForms) => [
      ...prevForms,
      {
        data: [],
        columns: [],
        columnVisibility: {},
      },
    ]);
    setCurrentFormIndex(forms.length);
  };

  const resetForms = () => {
    setForms([
      {
        data: [],
        columns: [],
        columnVisibility: {},
      },
    ]);
    setCurrentFormIndex(0);
  };

  const calculateTotal = (formIndex) => {
    const form = forms[formIndex];
    let calculatedTotal = {};
    form.columns.forEach((col) => {
      calculatedTotal[col] = 0;
    });
    form.data.forEach((item) => {
      form.columns.forEach((col) => {
        calculatedTotal[col] += parseFloat(item[col]) || 0;
      });
    });

    setForms((prevForms) => {
      const updatedForms = [...prevForms];
      updatedForms[formIndex].columnVisibility = calculatedTotal;
      return updatedForms;
    });
  };

  return (
    <div className="App">
      <h1>Cost Calculator</h1>
      <button onClick={createNewForm}>Create New Form</button>
      <button onClick={resetForms}>Start Over</button>
      {forms.map((form, formIndex) => (
  <div key={formIndex}>
    <h2>Form {formIndex + 1}</h2>
    <table>
      <thead>
        <tr>
          {form.columns.map((column, colIndex) => (
            <th key={colIndex}>
              <div>
                <input
                  type="checkbox"
                  checked={form.columnVisibility[column]}
                  onChange={() => toggleColumnVisibility(formIndex, column)}
                />
                {column}
              </div>
            </th>
          ))}
        </tr>
      </thead>
      <tbody>
        {form.data.map((item, rowIndex) => (
          <tr key={rowIndex}>
            {form.columns.map((column, colIndex) => (
              <td key={colIndex}>
                {column === 'quantity' ? (
                  <input
                    type="number"
                    value={item[column]}
                    onChange={(e) => handleQuantityChange(formIndex, rowIndex, e.target.value)}
                  />
                ) : (
                  <input
                    type="text"
                    value={item[column]}
                    onChange={(e) => {
                      const updatedData = [...form.data];
                      updatedData[rowIndex][column] = e.target.value;
                      const updatedForms = [...forms];
                      updatedForms[formIndex].data = updatedData;
                      setForms(updatedForms);
                    }}
                  />
                )}
              </td>
            ))}
          </tr>
        ))}
      </tbody>
    </table>
    <button onClick={() => addNewColumn(formIndex)}>Add New Column</button>
    <button onClick={() => addNewEntry(formIndex)}>Add New Entry</button>
    <div>
      <h2>Totals</h2>
      <table>
        <tbody>
          <tr>
            {form.columns.map((column, colIndex) => (
              <td key={colIndex}>
                {form.columnVisibility[column] && (
                  <div>
                    {column === 'quantity' ? (
                      <input
                        type="number"
                        value={form.columnVisibility[column]}
                        readOnly
                      />
                    ) : (
                      <input
                        type="text"
                        value={form.columnVisibility[column]}
                        readOnly
                      />
                    )}
                  </div>
                )}
              </td>
            ))}
          </tr>
        </tbody>
      </table>
    </div>
    <button onClick={() => calculateTotal(formIndex)}>Calculate Totals</button>
  </div>


      ))}
    </div>
  );
}

export default App;