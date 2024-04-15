import React, { useState } from 'react';
import { PDFDownloadLink, Document, Page, Text, View, StyleSheet } from '@react-pdf/renderer';

// PDF templates
const BtechTemplate = ({ name, date }) => (
  <Document>
    <Page style={styles.page}>
      <View>
        <Text style={styles.text}>Offer Letter</Text>
        <Text style={styles.text}>Date of Offer: {date}</Text>
        <Text style={styles.text}>Name: {name}</Text>
        <Text style={styles.text}>Course: B.tech</Text>
      </View>
    </Page>
  </Document>
);

const MtechTemplate = ({ name, date }) => (
  <Document>
    <Page style={styles.page}>
      <View>
        <Text style={styles.text}>Offer Letter</Text>
        <Text style={styles.text}>Date of Offer: {date}</Text>
        <Text style={styles.text}>Name: {name}</Text>
        <Text style={styles.text}>Course: M.tech</Text>
      </View>
    </Page>
  </Document>
);

// Form component
const Form = () => {
  const [name, setName] = useState('');
  const [course, setCourse] = useState('B.tech');

  const handleNameChange = (e) => {
    setName(e.target.value);
  };

  const handleCourseChange = (e) => {
    setCourse(e.target.value);
  };

  const currentDate = new Date().toLocaleDateString();

  return (
    <div>
      <form>
        <label>
          Name:
          <input type="text" value={name} onChange={handleNameChange} />
        </label>
        <label>
          Course:
          <select value={course} onChange={handleCourseChange}>
            <option value="B.tech">B.tech</option>
            <option value="M.tech">M.tech</option>
          </select>
        </label>
      </form>
      {course === 'B.tech' ? (
        <PDFDownloadLink document={<BtechTemplate name={name} date={currentDate} />} fileName="BtechOfferLetter.pdf">
          {({ blob, url, loading, error }) => (loading ? 'Generating PDF...' : 'Download PDF')}
        </PDFDownloadLink>
      ) : (
        <PDFDownloadLink document={<MtechTemplate name={name} date={currentDate} />} fileName="MtechOfferLetter.pdf">
          {({ blob, url, loading, error }) => (loading ? 'Generating PDF...' : 'Download PDF')}
        </PDFDownloadLink>
      )}
    </div>
  );
};

const styles = StyleSheet.create({
  page: {
    flexDirection: 'row',
    backgroundColor: '#E4E4E4',
    padding: 10,
  },
  text: {
    fontSize: 12,
    marginBottom: 10,
  },
});

export default Form;
