<%*
const fetchPopulation = async (country) => {
    try {
        // Construct the API request
        const response = await fetch(`https://get-population.p.rapidapi.com/population/country?country=${country}`, {
            method: 'GET',
            headers: {
                'x-rapidapi-key': 'a4138c88e9msh4c846aa1d2beb64p18e1f8jsn52ce8364c9d2',
                'x-rapidapi-host': 'get-population.p.rapidapi.com'
            }
        });

        console.log('Response status:', response.status); // Log the status code
        console.log('Response headers:', response.headers); // Log the headers

        // Parse the response data
        const data = await response.json();
        console.log('Response data:', data); // Log the full response for debugging

        // Check if the population data is present
        if (data && data.count) {
            return data.readable_format ? data.readable_format : data.count.toLocaleString();
        } else {
            throw new Error(`No population data found for ${country}. Data returned: ${JSON.stringify(data)}`);
        }
    } catch (error) {
        console.error('Fetch error:', error);
        return null;
    }
};

// Prompt for the country name
const country = await tp.system.prompt("Enter the country name");
if (country) {
    const population = await fetchPopulation(country);
    if (population) {
        tR += `### Population of ${country}\n\n`;
        tR += `- **Population**: ${population}\n\n`;
    } else {
        tR += `Error: Could not retrieve population data for ${country}.\n\n`;
    }
} else {
    tR += `Error: No country name entered.\n\n`;
}
%>
